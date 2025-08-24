# **Payment Integration with PayPal - Documentation**

---

## **Table of Contents**

1. [Introduction](#introduction)
2. [Overview](#overview)
3. [Use Case Flows](#use-case-flows)

   * [Actors](#actors)
   * [Flow Cases](#flow-cases)

     * [1. Payment Completed Successfully](#1-payment-completed-successfully)
     * [2. Payment Failed](#2-payment-failed)
     * [3. Payment Cancelled by User](#3-payment-cancelled-by-user)
     * [4. Payment Authorized but Not Captured](#4-payment-authorized-but-not-captured)
     * [5. Refund After Successful Payment](#5-refund-after-successful-payment)
     * [6. User Abandons Payment](#6-user-abandons-payment)
4. [Pseudocode](#pseudocode)
5. [Entity Relationship Diagram (ERD)](#entity-relationship-diagram-erd)
6. [Data Model Description](#data-model-description)
7. [Database Schema (PostgreSQL Compatible)](#database-schema-postgresql-compatible)

---

## **Introduction**

This document describes the integration of **PayPal payment** in the booking platform for hotel and flight reservations. It explains how payments are processed, tracked, and recorded using the **Strategy design pattern** to support multiple providers in the future.

The documentation includes:

* Overview of payment flows
* Detailed use case scenarios
* Pseudocode examples
* Entity Relationship Diagram (ERD)
* Database models and PostgreSQL-compatible schema

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
