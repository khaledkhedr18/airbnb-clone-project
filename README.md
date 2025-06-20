# Airbnb Clone – Backend

## Overview

The Airbnb Clone is a backend project developed as part of the ALX Software Engineering Program. It aims to replicate the core features of the Airbnb platform, including user management, property listings, booking functionality, payments, and reviews. The backend is designed to be scalable, maintainable, and easy to integrate with front-end and third-party services.

## Project Goals

- **User Management**: Implement secure registration, authentication, and profile management.
- **Property Management**: Allow hosts to create, update, and manage property listings.
- **Booking System**: Enable users to book properties and manage their reservations.
- **Payment Processing**: Integrate payment workflows for secure transaction handling.
- **Review System**: Let users leave reviews and ratings for properties.
- **Performance Optimization**: Improve performance through database indexing and caching strategies.

## Tech Stack

- **Framework**: Django
- **API Development**: Django REST Framework, GraphQL, OpenAPI (Swagger)
- **Database**: PostgreSQL
- **Asynchronous Task Queue**: Celery
- **Caching and Session Management**: Redis
- **Containerization**: Docker
- **CI/CD Pipelines**: Automated workflows for testing and deployment

## Team Roles

A successful project depends on clearly defined roles and responsibilities. The Airbnb Clone backend project includes the following key roles:

### Backend Developer

Responsible for designing, implementing, and maintaining the API endpoints, business logic, and integration of core features such as user authentication, property management, booking, payments, and reviews. They ensure the application logic is aligned with the project requirements and is scalable and secure.

### Database Administrator (DBA)

Manages the structure, performance, and integrity of the database. This includes designing schemas, creating indexes for optimization, performing backups, and ensuring data security. In this project, the DBA ensures PostgreSQL is optimized for handling large volumes of user and property data.

### DevOps Engineer

Handles the infrastructure and deployment pipeline of the application. Responsible for setting up Docker containers, managing CI/CD pipelines, monitoring server performance, and ensuring high availability and scalability of backend services. DevOps also configures Redis, Celery, and manages cloud deployments if applicable.

### QA Engineer

Ensures the reliability and quality of the backend system by writing automated tests, performing manual testing, and validating each feature against its requirements. The QA engineer is also responsible for reporting bugs, verifying bug fixes, and supporting regression testing across the system.

## Technology Stack

The backend of the Airbnb Clone project leverages modern and widely-used technologies to ensure robustness, scalability, and maintainability. Below is an overview of each technology and its role in the system:

### Django

A high-level Python web framework used to build the core of the application. It provides the structure for models, views, and controllers (MVC) and handles URL routing, request handling, and integrates seamlessly with the database.

### Django REST Framework (DRF)

A powerful toolkit built on top of Django for building Web APIs. It simplifies the creation of RESTful endpoints that handle CRUD operations for users, properties, bookings, reviews, and payments.

### GraphQL

An alternative API query language that allows clients to request exactly the data they need. It provides flexibility in how frontend applications interact with backend data.

### PostgreSQL

A powerful open-source relational database system used for structured data storage. It supports complex queries and relationships between entities like users, properties, and bookings.

### Celery

An asynchronous task queue used to handle background tasks such as sending confirmation emails, processing payments, or handling delayed actions outside of the main request-response cycle.

### Redis

An in-memory data structure store used as a message broker for Celery and for caching frequently accessed data, improving overall performance and reducing database load.

### Docker

A containerization platform used to package the application and its dependencies into containers, ensuring consistent development, testing, and production environments.

### CI/CD Pipelines

Automated tools and scripts (e.g., GitHub Actions, GitLab CI) used to test, build, and deploy the application whenever changes are pushed to the codebase. This ensures continuous integration and rapid delivery of new features and bug fixes.

## Database Design

The backend database schema is designed to support core functionalities such as user management, property listings, booking flow, reviews, and payments. Below are the main entities, their key fields, and how they relate to each other.

### 1. Users

Represents individuals using the platform, including both guests and hosts.

**Key Fields:**

- `id`: Unique identifier for the user
- `username`: User's login name
- `email`: Contact email (unique)
- `password_hash`: Encrypted password
- `is_host`: Boolean indicating whether the user can list properties

**Relationships:**

- A user can own multiple properties
- A user can make multiple bookings
- A user can leave multiple reviews

---

### 2. Properties

Represents properties listed by hosts for booking.

**Key Fields:**

- `id`: Unique identifier for the property
- `title`: Name/title of the property
- `description`: Detailed info about the property
- `location`: Address or city
- `price_per_night`: Cost per night

**Relationships:**

- A property belongs to one user (host)
- A property can have many bookings
- A property can receive multiple reviews

---

### 3. Bookings

Represents a reservation made by a user for a property.

**Key Fields:**

- `id`: Unique identifier for the booking
- `user_id`: Foreign key to the user who made the booking
- `property_id`: Foreign key to the booked property
- `check_in`: Start date of booking
- `check_out`: End date of booking

**Relationships:**

- A booking is linked to one user and one property
- A booking may be associated with one payment

---

### 4. Reviews

Represents user feedback and ratings for properties.

**Key Fields:**

- `id`: Unique identifier for the review
- `user_id`: Reviewer (foreign key to user)
- `property_id`: Reviewed property
- `rating`: Numeric rating (e.g., 1 to 5)
- `comment`: Optional text feedback

**Relationships:**

- A review is created by one user for one property
- A property can have many reviews

---

### 5. Payments

Handles transaction records related to bookings.

**Key Fields:**

- `id`: Unique identifier for the payment
- `booking_id`: Related booking
- `amount`: Total amount paid
- `payment_method`: e.g., card, PayPal
- `payment_status`: e.g., pending, completed

**Relationships:**

- A payment belongs to one booking
- A booking has one payment record
