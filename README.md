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
1. **Customer (Guest / User)**

   * Books hotels or flights.
   * Manages bookings, payments, cancellations, and refunds.

2. **Hotel Supplier**

   * Manages hotel listings, room availability, pricing.
   * Handles booking confirmations, modifications, and cancellations.

3. **Airline Supplier**

   * Provides flight schedules, seat availability, and fares.
   * Confirms or rejects flight bookings.

4. **Payment Provider (e.g., PayPal, Visa, Mastercard, Apple Pay)**

   * Handles online payment authorization, capture, refunds.

5. **Administrator (Platform Admin)**

   * Manages users, suppliers, listings, disputes, promotions, refunds.
   * Ensures compliance (licenses, policies, fraud prevention).
     
6. **Customer Service** 

   * Assists customers with booking issues, cancellations, and refunds.
   * Assists suppliers with registration, listing issues, availability updates, settlement disputes.
   * Resolving conflicts between customer and supplier.

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

