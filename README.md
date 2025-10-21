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

## Feature Breakdown

The Airbnb Clone Project is structured around key functional modules that simulate a real-world property rental platform. Each feature is designed to support both user experience and business logic consistency.

### 1. User Management
Handles user registration, authentication, and profile management. It ensures secure account access and enables users to manage personal details, view their bookings, and interact with the platform.

### 2. Property Management
Allows property owners to list, update, and manage their properties. Includes functionality for adding property details such as title, description, location, pricing, and availability, forming the core of the application’s content.

### 3. Booking System
Facilitates the reservation process between users and property owners. It manages booking creation, modification, and cancellation, ensuring proper validation of availability and payment confirmation.

### 4. Review and Rating System
Enables users to provide feedback on properties after their stay. Reviews help maintain platform credibility and assist future guests in making informed decisions.

### 5. Payment Processing
Integrates secure payment gateways for handling booking payments. It manages payment authorization, transaction logging, and verification to ensure reliable and transparent financial operations.

### 6. Search and Filtering
Allows users to search for properties using various filters such as location, price range, amenities, and availability. This feature enhances usability and improves the user’s ability to find relevant listings efficiently.

### 7. Admin Dashboard
Provides administrators with tools to monitor platform activity, manage users, properties, and resolve disputes. It serves as the control center for maintaining platform integrity and enforcing policies.


## API Security

Securing the backend APIs is critical to protect user data, maintain system integrity, and prevent unauthorized access to the platform. The Airbnb Clone Project implements multiple layers of security to ensure that all transactions and interactions are protected.

### 1. Authentication
User authentication is required for all protected endpoints using JSON Web Tokens (JWT). This ensures that only verified users can access or modify data related to their accounts, properties, and bookings.

**Importance:**  
Prevents unauthorized access to sensitive user data and ensures actions are traceable to legitimate users.

---

### 2. Authorization
Role-based access control (RBAC) determines what actions each type of user can perform (e.g., admin, host, guest). It enforces boundaries such as preventing guests from modifying property listings or accessing admin endpoints.

**Importance:**  
Ensures users can only perform actions permitted by their roles, reducing data tampering and privilege abuse.

---

### 3. Data Validation and Sanitization
All API inputs are validated and sanitized to prevent injection attacks such as SQL injection or cross-site scripting (XSS). This ensures only correctly formatted and safe data enters the system.

**Importance:**  
Prevents malicious input from compromising the database or the overall application security.

---

### 4. HTTPS and Encryption
All communication between the client and server occurs over HTTPS, and sensitive information (like passwords) is stored using strong hashing algorithms such as bcrypt.

**Importance:**  
Protects data in transit and at rest from interception and unauthorized access.

---

### 5. Rate Limiting and Throttling
Implements request rate limiting to restrict the number of API calls a user can make within a given time window. This mitigates denial-of-service (DoS) and brute-force attacks.

**Importance:**  
Prevents abuse of API endpoints and maintains service availability for legitimate users.

---

### 6. Secure Payment Processing
Integrates with trusted third-party payment gateways that adhere to PCI DSS standards. Payment-related data is never stored directly on the platform.

**Importance:**  
Protects users’ financial information and reduces liability in the event of security incidents.


## CI/CD Pipeline

Continuous Integration (CI) and Continuous Deployment (CD) are development practices that automate the process of building, testing, and deploying code. CI/CD pipelines ensure that every code change is automatically validated and deployed in a consistent and reliable manner.

### Purpose of CI/CD
The CI/CD pipeline helps maintain code quality by running automated tests and security checks before merging changes. It also reduces deployment errors by automating the build and release process, allowing developers to deliver new features and fixes rapidly without manual intervention.

### Tools Used
- **GitHub Actions:** Automates testing, linting, and deployment workflows directly from the GitHub repository.  
- **Docker:** Ensures consistent runtime environments by containerizing the application for development, testing, and production.  
- **Docker Hub:** Serves as a repository for storing and distributing Docker images used across different environments.  
- **AWS or Heroku:** Provides hosting and scalable infrastructure for automatic deployment from the CI/CD pipeline.

### Benefits
- Faster and more reliable deployments.  
- Early detection of integration issues.  
- Improved collaboration through automated testing and code validation.  
- Consistency between development, staging, and production environments.

