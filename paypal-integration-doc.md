# **Payment Integration with PayPal - Documentation**

This document describes the integration of **PayPal payment** in the booking platform for hotel and flight reservations. It explains how payments are processed, tracked, and recorded using the **Strategy design pattern** to support multiple providers in the future.

The documentation includes:

* Overview of payment flows
* Detailed use case scenarios
* Pseudocode examples
* Entity Relationship Diagram (ERD)
* Database models and PostgreSQL-compatible schema
  
---

## **Table of Contents**

1. [Overview](#overview)
2. [Use Case Flows](#use-case-flows)

   * [Actors](#actors)
   * [Flow Cases](#flow-cases)

     * [1. Payment Completed Successfully](#1-payment-completed-successfully)
     * [2. Payment Failed](#2-payment-failed)
     * [3. Payment Cancelled by User](#3-payment-cancelled-by-user)
     * [4. Payment Authorized but Not Captured](#4-payment-authorized-but-not-captured)
     * [5. Refund Flow](#5-refund-flow)
     * [6. User Abandons Payment](#6-user-abandons-payment)
3. [Pseudocode](#pseudocode)
4. [Entity Relationship Diagram (ERD)](#entity-relationship-diagram-erd)
5. [Data Model Description](#data-model-description)
6. [Database Schema (PostgreSQL Compatible)](#database-schema-postgresql-compatible)

---

## **Overview**

The payment integration supports:

* PayPal payment flow (authorize, capture, refund)
* Transaction tracking for each booking
* Webhook handling for real-time payment updates
* Ability to extend to other payment providers

**Key concepts:**

* **Transaction**: Each payment attempt linked to a booking
* **Booking**: Represents hotel/flight reservation
* **Webhook**: Real-time notification from PayPal for payment/capture/refund events

---

## **Use Case Flows**

### **Actors**

* **Frontend (User Interface)**

  * Displays booking and payment options
  * Initiates payment requests to the backend
  * Redirects the user to PayPal for approval
  * Shows success, failure, or cancellation messages after payment

* **Backend (PaymentController, PaymentService, StrategyFactory)**

  * Handles all API requests from the frontend
  * Creates and updates booking records
  * Manages payment transactions
  * Selects the correct payment provider strategy (e.g., PayPal)
  * Calls external APIs (PayPal) and processes webhooks

* **PayPal (External Payment Gateway)**

  * Provides approval UI for the customer
  * Handles authentication and payment authorization/capture
  * Sends webhooks for order, capture, authorization, and refund events

* **Database (Persistence Layer)**

  * Stores booking records with current status (e.g., PENDING, CONFIRMED, CANCELLED)
  * Stores payment transactions and their lifecycle states (PENDING, AUTHORIZED, COMPLETED, FAILED, ABANDONED, REFUNDED)
  * Stores refund requests and results
  * Ensures consistency between booking lifecycle and payment lifecycle

***

### **Flow Cases**

#### **1. Payment Completed Successfully**

**Goal:** Complete the payment and confirm booking.

**Precondition:** User has a valid booking and chooses PayPal.

**Flow Steps:**

1. User clicks "Pay with PayPal".
2. Frontend sends `POST /payments/process` with booking details.
3. Backend creates booking (`PENDING_PAYMENT`) and transaction (`PENDING`).
4. Backend calls PayPal `/v2/checkout/orders` (intent=CAPTURE).
5. PayPal returns `order_id` and `approval_url`.
6. Backend updates transaction with `order_id` and `approval_url`.
7. Frontend redirects user to `approval_url`.
8. User approves payment on PayPal UI.
9. PayPal redirects user to `returnUrl`.
10. PayPal sends webhook `PAYMENT.CAPTURE.COMPLETED`.
11. Backend verifies webhook and updates transaction (`COMPLETED`) and booking (`CONFIRMED`).
12. User sees booking confirmation.

**Postcondition:** Transaction = COMPLETED, Booking = CONFIRMED

___

#### **2. Payment Failed**

**Goal:** Handle declined payment.

**Precondition:** User attempts payment with insufficient funds or invalid card.

**Flow Steps:**

1. User clicks "Pay with PayPal".
2. Backend creates booking (`PENDING_PAYMENT`) and transaction (`PENDING`).
3. Backend requests PayPal order.
4. User attempts payment; PayPal declines.
5. PayPal sends webhook `PAYMENT.CAPTURE.DENIED`.
6. Backend updates transaction (`FAILED`) and booking (`FAILED`).
7. Frontend notifies user: Payment failed.

**Postcondition:** Transaction = FAILED, Booking = FAILED

---

#### **3. Payment Cancelled by User**

**Goal:** Handle user cancellation during PayPal checkout.

**Precondition:** User initiates payment.

**Flow Steps:**

1. User clicks "Pay with PayPal".
2. Backend creates booking (`PENDING_PAYMENT`) and transaction (`PENDING`).
3. Backend requests PayPal order.
4. User cancels on PayPal UI.
5. PayPal redirects to `cancelUrl`.
6. Backend updates transaction (`CANCELLED_BY_USER`) and booking (`CANCELLED`).
7. Frontend notifies user: Payment cancelled.

**Postcondition:** Transaction = CANCELLED\_BY\_USER, Booking = CANCELLED

---

#### **4. Payment Authorized but Not Captured**

**Goal:** Authorize payment first, capture later.

**Precondition:** Merchant uses delayed capture (e.g., hotel pre-check-in).

**Flow Steps:**

1. User clicks "Pay with PayPal".
2. Backend creates booking (`PENDING_PAYMENT`) and transaction (`PENDING`).
3. Backend requests PayPal order (intent=AUTHORIZE).
4. PayPal returns `order_id` and `approval_url`.
5. Frontend redirects user.
6. User approves on PayPal UI.
7. PayPal authorizes funds; sends `PAYMENT.AUTHORIZATION.CREATED`.
8. Backend updates transaction (`AUTHORIZED`) and booking (`AUTHORIZED`).
9. Later, backend calls PayPal to capture authorization.
10. PayPal processes capture; sends webhook `PAYMENT.CAPTURE.COMPLETED`.
11. Backend updates transaction (`COMPLETED`) and booking (`CONFIRMED`).
12. If authorization expires, webhook `PAYMENT.AUTHORIZATION.VOIDED` updates transaction (`EXPIRED`) and booking (`EXPIRED_AUTHORIZATION`).

**Postcondition:** Transaction = AUTHORIZED or COMPLETED, Booking = AUTHORIZED or CONFIRMED

---

#### **5. Refund Flow**

**Goal:** Refund payment after cancellation.

**Precondition:** Booking already paid and eligible for refund.

**Flow Steps:**

1. User requests refund via frontend.
2. Backend creates refund record (`PENDING`) linked to transaction.
3. Backend calls PayPal Refund API.
4. PayPal processes refund; sends webhook `PAYMENT.REFUND.COMPLETED`.
5. Backend updates refund (`COMPLETED`), transaction (`REFUNDED`), and booking (`REFUNDED`).
6. Frontend notifies user: Refund processed.

**Postcondition:** Transaction = REFUNDED, Booking = REFUNDED

---

#### **6. User Abandons Payment**

**Goal:** Handle the scenario where the user starts the payment but leaves the checkout without completing it.

**Precondition:**

* User has initiated a booking and clicked “Pay with PayPal.”
* A transaction record with status `PENDING` exists.

**Flow Steps:**

1. User clicks “Pay with PayPal.”
2. Backend creates booking (`PENDING_PAYMENT`) and transaction (`PENDING`).
3. Backend requests PayPal order; receives `order_id` and `approval_url`.
4. Backend updates transaction with `order_id` and `approval_url`.
5. Frontend redirects user to PayPal UI.
6. User abandons the payment (closes tab, navigates away, or does not approve).
7. No webhook is sent because the payment is never approved.
8. Backend can optionally implement a **timeout mechanism** (e.g., 30 minutes) to mark transactions as **ABANDONED**.
9. Database updates transaction (`ABANDONED`) and booking (`PAYMENT_TIMEOUT` or `PENDING_PAYMENT_EXPIRED`).
10. Frontend may notify user: “Payment was not completed. Please try again.”

**Postcondition:**

* Transaction = ABANDONED
* Booking = PAYMENT\_TIMEOUT / PENDING\_PAYMENT\_EXPIRED

---
