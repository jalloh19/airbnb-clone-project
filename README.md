# Airbnb Clone Project

## Overview
The Airbnb Clone Project is a full-stack web application designed to replicate the core functionalities of Airbnb.

## Project Goals
- Build a scalable and secure web application.
- Implement modern backend development practices using Django and MySQL.
- Gain practical experience with API design, authentication, and deployment workflows.

## Technology Stack
- Django (Backend Framework)
- MySQL (Relational Database)
- GraphQL (API Query Language)
- Docker (Containerization)
- GitHub Actions (CI/CD)

## Database Design

The Airbnb Clone Project uses a relational database to store structured data about users, properties, bookings, reviews, and payments. The relationships are designed to ensure data integrity and efficient queries.

### Entities and Attributes

#### 1. Users
- `id`: Primary key, unique user identifier  
- `username`: Unique username for authentication  
- `email`: Contact email address  
- `password_hash`: Encrypted password for security  
- `date_joined`: Timestamp of account creation  

**Relationships:**  
A user can own multiple properties and make multiple bookings.

---

#### 2. Properties
- `id`: Primary key, unique property identifier  
- `owner_id`: Foreign key referencing `Users.id`  
- `title`: Name or title of the property  
- `description`: Text describing the property  
- `price_per_night`: Decimal value for nightly rate  

**Relationships:**  
Each property belongs to one user (owner). A property can have multiple bookings and reviews.

---

#### 3. Bookings
- `id`: Primary key, unique booking identifier  
- `user_id`: Foreign key referencing `Users.id`  
- `property_id`: Foreign key referencing `Properties.id`  
- `check_in`: Date of arrival  
- `check_out`: Date of departure  

**Relationships:**  
A booking belongs to one user and one property. Each booking can have an associated payment.

---

#### 4. Reviews
- `id`: Primary key, unique review identifier  
- `property_id`: Foreign key referencing `Properties.id`  
- `user_id`: Foreign key referencing `Users.id`  
- `rating`: Integer value (1–5)  
- `comment`: Text feedback  

**Relationships:**  
A review is made by a user for a specific property.

---

#### 5. Payments
- `id`: Primary key, unique payment identifier  
- `booking_id`: Foreign key referencing `Bookings.id`  
- `amount`: Total payment amount  
- `payment_status`: Enum (e.g., “Pending”, “Completed”, “Failed”)  
- `transaction_date`: Timestamp of payment  

**Relationships:**  
Each payment is linked to one booking.

---

### Entity Relationships Summary
- A **User** can have many **Properties**.  
- A **User** can make many **Bookings**.  
- A **Property** can have many **Bookings** and **Reviews**.  
- A **Booking** is associated with one **Property** and one **User**.  
- A **Payment** belongs to one **Booking**.

