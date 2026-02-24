# Job Tracker API

A multi-user backend API to manage job applications, companies and
hiring interactions.

This project demonstrates how to design and build a clean, secure and
scalable Spring Boot backend using modern enterprise practices.

------------------------------------------------------------------------

## 🚀 Overview

Job Tracker is a RESTful API that allows authenticated users to:

-   Manage companies they have applied to
-   Track job applications and their status
-   Log interactions (emails, interviews, calls, offers)
-   Work in a secure multi-user environment with role-based access
    control

Each user only has access to their own data.

------------------------------------------------------------------------

## 🏗 Architecture

The project follows a clean layered architecture:

com.acido303.jobtracker\
├── api \# REST controllers, DTOs, error handling\
├── application \# Use cases and business services\
├── domain \# Core domain models and business rules\
├── infrastructure \# Persistence, security, configuration

### Key Principles

-   Separation of concerns
-   Domain-driven structure
-   Role-based access control (RBAC)
-   Database versioning with Liquibase
-   Auditing with `createdBy` and `createdAt`
-   Consistent API error responses (RFC 7807 style)

------------------------------------------------------------------------

## 🛠 Tech Stack

-   Java 21
-   Spring Boot
-   Spring Security (Basic Auth)
-   Spring Data JPA
-   PostgreSQL
-   Liquibase
-   OpenAPI / Swagger
-   Testcontainers
-   Docker

------------------------------------------------------------------------

## 🔐 Security Model

-   HTTP Basic Authentication
-   Passwords stored using BCrypt (I want this to work without external dependency on any other service)
-   Role-based access control:
    -   ROLE_USER
    -   ROLE_ADMIN
-   Multi-user data isolation (users only see their own records)
-   Automatic auditing (createdBy, createdAt)

------------------------------------------------------------------------

## 📦 Domain Model

### User

-   Managed via database
-   Linked to roles through a many-to-many relationship

### Company

-   Represents a company applied to
-   Unique per user

### Job

-   Linked to a company
-   Tracks status: APPLIED, SCREENING, INTERVIEW, OFFER, REJECTED, WITHDRAWN

### Interaction

-   Linked to a job
-   Represents communication or hiring steps

------------------------------------------------------------------------

## 📚 API Documentation

Swagger UI:

http://localhost:8080/swagger-ui.html

OpenAPI spec:

http://localhost:8080/v3/api-docs

------------------------------------------------------------------------

## ▶️ Running Locally

### 1. Start PostgreSQL

docker compose up -d

### 2. Run the application

mvn spring-boot:run

------------------------------------------------------------------------

## 🧪 Running Tests

mvn clean verify

Integration tests use Testcontainers to spin up a PostgreSQL container
automatically.

------------------------------------------------------------------------

## 🗄 Database Versioning

Database schema is managed with Liquibase.

Changelogs are located in:

src/main/resources/db/changelog

------------------------------------------------------------------------

## 📌 Design Decisions

-   UUIDs used for entity identifiers (cloud-friendly and distributed-safe)
-   Roles stored in a dedicated table (proper RBAC model)
-   Auditing handled via Spring Data JPA
-   Controllers kept thin; business logic in application layer
-   Explicit repository filtering instead of hidden Hibernate filters

------------------------------------------------------------------------

## 🧭 Future Improvements

-   JWT authentication
-   Pagination & sorting
-   Role-based endpoint restrictions
-   CI pipeline with coverage reporting
-   Observability (metrics, tracing)

------------------------------------------------------------------------

## 📄 License

This project is licensed under the MIT License.

This repository is intended for demonstration and educational purposes.
