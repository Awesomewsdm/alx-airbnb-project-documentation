# Airbnb Clone - Backend Requirement Specifications

This document outlines the **technical and functional requirements** for key backend features of the Airbnb Clone project.

---

## 1. User Authentication

### Description
Handles user registration, login, and session management. Supports guests, hosts, and admins.

### API Endpoints
- `POST /api/v1/auth/register` — Register a new user
- `POST /api/v1/auth/login` — Authenticate user and return JWT token
- `GET /api/v1/auth/profile` — Retrieve user profile (authenticated)
- `PUT /api/v1/auth/profile` — Update user profile (authenticated)

### Input/Output Specification
**Register Request:**
```json
{
  "first_name": "John",
  "last_name": "Doe",
  "email": "john@example.com",
  "password": "securePassword123"
}
```

**Register Response:**
```json
{
  "user_id": "uuid",
  "email": "john@example.com",
  "role": "guest",
  "token": "jwt_token_here"
}
```

**Validation Rules:**
- Email must be unique and valid format
- Password must be at least 8 characters
- Required fields: first_name, last_name, email, password

**Performance Criteria:**
- Token generation and validation must occur in <200ms
- System must handle at least 100 login requests per second

---

## 2. Property Management

### Description
Allows hosts to add, update, and delete property listings.

### API Endpoints
- `POST /api/v1/properties` — Create new property (host only)
- `GET /api/v1/properties` — List properties with filters
- `GET /api/v1/properties/:id` — Retrieve property details
- `PUT /api/v1/properties/:id` — Update property details (host only)
- `DELETE /api/v1/properties/:id` — Delete property (host only)

### Input/Output Specification
**Add Property Request:**
```json
{
  "name": "Cozy Apartment",
  "description": "2-bedroom apartment in Accra",
  "location": "Accra",
  "price_per_night": 50.00,
  "amenities": ["WiFi", "Air Conditioning"]
}
```

**Property Response:**
```json
{
  "property_id": "uuid",
  "host_id": "uuid",
  "name": "Cozy Apartment",
  "location": "Accra",
  "price_per_night": 50.00,
  "status": "active"
}
```

**Validation Rules:**
- Price must be > 0
- Location and description cannot be empty
- Only authenticated hosts can create/edit/delete properties

**Performance Criteria:**
- Property retrieval must support pagination (max 50 per page)
- API should respond within 500ms for filtered searches

---

## 3. Booking System

### Description
Allows guests to book properties, check availability, and manage bookings.

### API Endpoints
- `POST /api/v1/bookings` — Create a new booking
- `GET /api/v1/bookings/:id` — Retrieve booking details
- `PUT /api/v1/bookings/:id/cancel` — Cancel a booking
- `GET /api/v1/bookings/user/:user_id` — Retrieve all bookings for a user

### Input/Output Specification
**Create Booking Request:**
```json
{
  "property_id": "uuid",
  "user_id": "uuid",
  "start_date": "2025-09-01",
  "end_date": "2025-09-05"
}
```

**Booking Response:**
```json
{
  "booking_id": "uuid",
  "status": "pending",
  "total_price": 200.00,
  "created_at": "2025-08-31T12:00:00Z"
}
```

**Validation Rules:**
- End date must be after start date
- Property must not have overlapping bookings
- Only authenticated users can make bookings

**Performance Criteria:**
- Availability checks must run in <300ms
- Must handle at least 50 booking requests per second

---

## Notes

- All endpoints must follow RESTful standards
- JWT authentication is required for protected routes
- Role-based access control (RBAC) applies: Guest, Host, Admin