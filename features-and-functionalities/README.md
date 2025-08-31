# Airbnb Clone - Features and Functionalities

This document provides an overview of the key features and backend functionalities of the Airbnb Clone project.

## Core Features
1. **User Management**
   - Registration (guest, host)
   - Authentication (JWT, OAuth)
   - Profile updates

2. **Property Listings**
   - Add, edit, delete listings
   - Include title, description, location, price, amenities, availability

3. **Search and Filtering**
   - Filter by location, price, guests, amenities
   - Pagination for large datasets

4. **Booking System**
   - Create, cancel bookings
   - Prevent double bookings
   - Track booking status (pending, confirmed, canceled, completed)

5. **Payment Integration**
   - Secure payments (Stripe, PayPal)
   - Multi-currency support
   - Automatic payouts to hosts

6. **Reviews and Ratings**
   - Guests leave reviews & ratings
   - Hosts respond to reviews
   - Reviews tied to bookings

7. **Notifications**
   - Email and in-app alerts for confirmations, cancellations, payments

8. **Admin Dashboard**
   - Monitor/manage users, listings, bookings, payments

## Technical Requirements
- Relational database (PostgreSQL/MySQL)
- REST APIs (+ optional GraphQL)
- Role-based access control (guest, host, admin)
- File storage for images (AWS S3, Cloudinary)
- Third-party services (SendGrid/Mailgun for email)
- Error handling and logging
- Caching (Redis)

## Non-Functional Requirements
- Scalability with load balancers
- Security (encryption, firewalls, rate limiting)
- Performance optimization
- Automated testing

## Diagram
See the diagram `features-and-functionalities.png` for a visual representation of all the above.
