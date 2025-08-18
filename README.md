# Booking (Hotel/Flight) Platform

## Content List

1. [Vision](#vision)
2. [Features and Functionalities for the System](#features-and-functionalities)
3. [Use Case Model for the System](#use-case-model-for-the-system)  
   3.1. [Actors](#actors)  
   3.2. [Use Cases](#use-cases)  
   3.3. [Use Case Diagram](#use-case-diagram)
---

## Vision  

The booking platform is designed to provide travelers with a seamless and intuitive experience for planning their trips. Users can effortlessly search for hotels and flights, compare options with ease, and complete bookings quickly and without complications. The platform also enables customers to manage their reservations, take advantage of exclusive deals, and enjoy reliable, secure payment processing tailored to their travel needs.

---

## Features and Functionalities for the System 

The detailed list of system features and functionalities is available in a separate document.  
Please refer to [Features and Functionalities Document](./features-documentation.md) for more details.

---

## Use Case Model for the System 

### `Actors of the System` 

| **Actor**                                                        | **Description**                                                                        | **Responsibilities**                                                                                                                                                                                                                                                                                         |
| ---------------------------------------------------------------- | -------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Customer (Guest / User)**                                      | End-user of the platform who books hotels or flights. Can be a traveler or local user. | - Search and book hotels/flights<br>- Manage bookings (view, modify, cancel)<br>- Make payments and request refunds<br>- Submit ratings/reviews<br>- Manage personal profile, preferences, and account settings                                                                                              |
| **Hotel Supplier**                                               | Hotel owner/manager who provides room inventory and manages hotel-related services.    | - Manage hotel property listings, room types, amenities, images, pricing<br>- Update availability, promotions, discounts<br>- Handle booking confirmations, modifications, and cancellations<br>- Manage settlement reports and financial reconciliation      |
| **Airline Supplier**                                             | Airline company providing flight schedules, fares, and seat inventory.                 | - Provide flight schedules, seat availability, and fares<br>- Confirm or reject booking requests<br>- Update flight status (delays, cancellations)<br>- Manage settlement and reconciliation<br>- Define fare rules, baggage policies, and refund rules                                                      |
| **Payment Provider (PayPal, Visa, Mastercard, Apple Pay, etc.)** | External service provider that processes customer payments.                            | - Handle payment authorization, capture, settlement, and refunds<br>- Provide transaction receipts and status updates<br>- Support fraud detection and dispute management<br>- Enable multi-currency and various payment methods                                                                             |
| **Administrator (Platform Admin)**                               | Internal role managing overall system operations and compliance.                       | - Manage customers, suppliers, and internal users<br>- Oversee listings, disputes, promotions, and refunds<br>- Ensure compliance with licenses, policies, and legal requirements<br>- Monitor financial reports and fraud prevention<br>- Generate dashboards and analytics reports                         |
| **Customer Service**                                             | Support role assisting customers and suppliers with issues.                            | - Help customers with booking, payment, cancellation, and refund issues<br>- Support suppliers with registration, listing setup, availability, pricing<br>- Resolve disputes between customers and suppliers<br>- Provide live chat, email, and phone support<br>- Escalate complex issues to administrators |

---

### `Main use cases` 
- **User Registration & Authentication**: 
   - Create User Account
   - Login
   - Logout
   - Forget Password
   - Get User Profile
   - Update user profile
   - Enable or Disable account
   - Verify Account [Email or SMS]
   - Social Media authentication
     
 - **Search & Filter**: 
   - Search Flights
   - Search Hotels
   - Filter Flights
   - Filter Hotels
   - Hotel Details
   - Flight Details
         
 - **Booking**: 
    - Book Hotel
    - Book Flight
    - Get Booking Details
    - Cancel Booking
    - Get Booking History
    - SMS or Email Confirmation booking [Notification]
      
 - **Notification**: 
    - Send Email or SMS confirmation
    - Push notification [Emails] for Offers
    - Subscribe to notification
  
 - **Customer Management**: 
    - Preferred Payment Setting
    - Address Management
    - Flight/hotel booking History
    - Rating/Review
    - Customer support [Chat]

 - **Payment Integration**: 
    - Payment Integration With third Party
    - View Payment History
    - Generate Payment Recipt
    - Auditing Payment Integration
    - Payment Verification
      
 - **Dashboard & Reporting [System]**: 
   - Count Customers
   - Count Active Customers
   - Daily count Flight/hotel Booking
   - Total count Order Flight/hotel
   - Daily Cancelled Booking Flight/hotel
   - Total Cancelled Booking Flight/hotel
   - Daily amount of transactions
   - Total amount of transactions
   - Generate Daily Transactions Report
   - Generate Monthly Transactions Report

### `Use Case Diagram` 

A visual representation of use cases and actors

![Booking Use Case Diagram](./diagrams/booking-use-case-modal.png) 

