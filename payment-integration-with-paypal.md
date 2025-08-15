# Payment Integration – Use Case Documentation

This repository contains comprehensive documentation for the **Payment Integration (with PayPal)** use case of a Hotel/Flight Booking Platform. It includes the complete flow description, visual representations, data modeling, and supporting pseudocode and diagrams.

---

## Content List

1. [Overview](#overview)
2. [Use Case Flows](#use-case-flows) 
3. [Flowchart Diagram](#flowchart-diagram)
4. [Sequence Diagram](#sequence-diagram)
5. [Pseudocode](#pseudocode)
6. [Entity Relationship Diagram (ERD)](#entity-relationship-diagram-erd)
7. [Data Model Description](#data-model-description)
8. [SQL Scripts](#sql-scripts)

---

## Overview

The PayPal integration allows customers to securely pay for hotel or flight bookings using their PayPal balance, linked bank account, or card, without sharing payment details with the platform.
Once authorized, the payment is confirmed, the booking is finalized, and a receipt containing both payment and booking details is provided.
This process ensures secure transactions, supports multi-currency payments, reduces compliance overhead, and streamlines settlement between the booking platform and its hotel or airline partners.
This documentation presents the full flow and core logic of the Place Order use case, including business rules, interaction diagrams, data entities, and implementation-ready pseudocode.

---

## Use Case Flows

### `Actors`  
- **Customer** – The traveler making the booking
- **Booking Platform** – The intermediary marketplace handling bookings and payments
- **PayPal** – The payment service provider facilitating secure transactions
- **Supplier (Hotel/Airline)** – The actual service provider
- **Payment Processors** – Banks or institutions that handle transaction settlement for merchants

### `Main Flow : Payment Flow with PayPal in a Booking Platform` 
#### Goal : 
Enable customers to pay for hotel or flight bookings using PayPal in a secure, reliable, and trackable manner.

#### **Precondition** : 
- Booking platform has integrated PayPal’s payment API.
- Customer has selected a service (hotel room, flight, etc.) and filled in booking details.
- Customer completes booking details (dates, room type, passenger info)
- Platform calculates total cost (base price + taxes + fees + surcharges)

#### **Flow Steps** : 
1. Customer selects PayPal from available payment options
2. Platform redirects to PayPal’s secure interface
3. Customer login to paypal account
4. PayPal displays booking details (platform name, amount, currency)
5. Customer selects funding source (bank account, credit card, PayPal balance)
6. PayPal runs real-time fraud screening
7. PayPal authorizes funds (but does not transfer yet)
8. PayPal sends authorization confirmation to the platform
9. Platform confirms booking with supplier & redirects customer back
10. Booking may be held until payment capture is completed
11. Confirmation page shows:
  - Booking reference & details
  - Payment reference
  - Receipt download link
 12. Automated confirmation email sent to customer
  - If later payment fails (e.g., chargeback), booking may be canceled with penalties
13. Platform captures payment from PayPal
14. PayPal moves funds to the platform’s merchant account
15. Funds remain there until withdrawn to the platform’s bank account
16. Platform settles payment with supplier (minus commission)
17. Supplier receives booking details and settlement

**Postcondition**:  
- Payment successfully processed and funds transferred
- Customer receives confirmed booking and receipt
- Supplier receives booking details and settlement

---

## Flowchart Diagram

![Place Order Flowchart](./diagrams/payment-integration-flowchart.png)

---

## Sequence Diagram

![FDS Sequence Diagram](./diagrams/payment-integration-sequence-diagram.png) 

---

## Pseudocode

 **Will be added soon.**

---

## Entity Relationship Diagram (ERD)

 **Will be added soon.**

---

## Data Model Description

 **Will be added soon.**

---

## Database Schema (PostgreSQL Compatible)

 **Will be added soon.**
