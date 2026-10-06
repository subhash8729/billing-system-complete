# Zosh POS System

A full-stack retail Point-of-Sale and store management system designed for multi-store operations. The project includes a Java Spring Boot backend, a React + Vite frontend, and MySQL-based persistence with role-based access for admins, store managers, branch managers, and cashiers.

## Overview

This application supports the end-to-end flow of running a retail operation, including:

- Store registration and onboarding
- User authentication and role management
- Product and category management
- Inventory tracking
- Customer handling
- Order creation and payment processing
- Refund handling
- Shift closing and sales reporting
- Store and branch analytics dashboards
- Subscription and plan management

## Tech Stack

### Backend
- Java 21
- Spring Boot 3.5.3
- Spring Web
- Spring Data JPA
- Spring Security + JWT authentication
- MySQL database
- Lombok
- Razorpay and Stripe integration
- Mail support for password reset and notifications

### Frontend
- React 19
- Vite
- Redux Toolkit
- React Router
- Tailwind CSS
- Recharts for dashboards and analytics
- Radix UI components

## Project Structure

```text
z-pos-source-code/
├── pos-backend/                  # Spring Boot backend
│   ├── src/main/java/com/zosh/   # Application code
│   ├── src/main/resources/       # application.yml and Docker config
│   ├── pom.xml                   # Maven configuration
│   ├── mvnw, mvnw.cmd            # Maven wrapper
│   └── HELP.md                   # Spring Boot starter help
│
├── pos-frontend-vite/            # React frontend
│   ├── src/                      # Application pages, routes, Redux slices
│   ├── public/                   # Static assets (if any)
│   ├── package.json              # Frontend dependencies and scripts
│   ├── vite.config.js            # Vite config
│   └── README.md                 # Default frontend template readme
│
└── README.md                     # Project documentation
```

## Core Features

### Authentication and Roles
The system supports multiple roles, including:

- ROLE_ADMIN
- ROLE_STORE_ADMIN
- ROLE_STORE_MANAGER
- ROLE_BRANCH_MANAGER
- ROLE_BRANCH_ADMIN
- ROLE_BRANCH_CASHIER

Authentication is implemented with JWT and is protected by Spring Security. Password reset functionality is also included.

### Store and Branch Management
- Store onboarding for admins and store users
- Store approval and moderation workflow
- Employee assignment to stores
- Branch-level operations and management

### Product and Inventory Management
- Product creation and updates
- Category-based organization
- Stock/inventory tracking
- Product-related reporting

### Sales and Payment Operations
- Order creation and checkout flow
- Payment processing with Stripe and Razorpay
- Refund management
- Shift summary and reporting

### Dashboards and Analytics
- Admin dashboard
- Store dashboard
- Branch analytics
- Sales and operational analytics

### Subscription Features
The backend contains subscription and subscription-plan modules for handling recurring retail service plans.

## Backend Configuration

The main Spring Boot configuration lives in:

- `pos-backend/src/main/resources/application.yml`

Key settings include:

- MySQL datasource
- Hibernate auto-update
- email configuration
- JWT-related placeholders
- Razorpay and Stripe API keys
- application server port `5000`

Example configuration:

```yaml
server:
  port: 5000

spring:
  datasource:
    url: jdbc:mysql://${DB_HOST:localhost}:${DB_PORT:3306}/${DB_NAME:pos-temp}
    username: ${DB_USERNAME:root}
    password: ${DB_PASSWORD:your-password}
```

## Running the Project

### 1) Start the database
You can use MySQL locally or run the included Docker Compose setup:

```bash
cd pos-backend/src/main/resources
docker compose up -d
```

The Docker configuration in `docker-compose.yml` provisions a MySQL service and exposes it on port `3301` for local development.

### 2) Run the backend
From the backend folder:

```bash
cd pos-backend
./mvnw clean install
./mvnw spring-boot:run
```

The backend runs on:

```text
http://localhost:5000
```

### 3) Run the frontend
From the frontend folder:

```bash
cd pos-frontend-vite
npm install
npm run dev
```

The frontend typically runs on:

```text
http://localhost:5173
```

## Environment Variables

The app expects the following values for runtime/database access:

```bash
DB_HOST=localhost
DB_PORT=3306
DB_NAME=pos-temp
DB_USERNAME=root
DB_PASSWORD=your-password
```

For payments and email features, configure:

```bash
RAZORPAY_KEY=your_razorpay_key
RAZORPAY_SECRET=your_razorpay_secret
STRIPE_KEY=your_stripe_key
```

## Docker Support

A basic Docker Compose file is included for running a MySQL database and the application environment. This is useful for local testing and containerized deployment.

## Notes

- The project is a monorepo-style setup with clearly separated backend and frontend apps.
- Frontend routing is role-aware and redirects users based on JWT and role detection.
- The backend is designed around REST APIs under `/api/*` and auth endpoints under `/auth/*`.
- This project is best suited for retail businesses or academic/demo environments focused on POS workflow automation.

## License

This project does not currently include a custom license file in the repository root. If you are publishing or distributing it, add an appropriate license before public release.

## Future Improvements

Potential improvements for this project include:

- Better environment configuration using `.env` files
- Service layer test coverage
- API documentation with Swagger/OpenAPI
- CI/CD setup
- Production-grade deployment configuration for Azure or Docker/Kubernetes
