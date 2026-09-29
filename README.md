# E-commerce Platform

A pet project demonstrating an e-commerce platform built with a microservices architecture using Spring Boot and React. The platform separates core e-commerce functionality, payment processing, and notifications into independent services.

## Features

- Product, user, and order management
- Payment processing through a dedicated payment service
- Notifications and messaging through a dedicated notification service
- React-based user interface built with Vite and hot module replacement
- JWT-based authentication
- Multilingual support for:
  - English
  - Romanian
  - Russian

## Architecture

The project contains the following services and modules:

| Module | Responsibility |
|---|---|
| Main Server (`ecommerce-platform-server`) | Core e-commerce functionality, including products, users, and orders |
| Payment Service (`ecommerce-platform-payment-service`) | Handles payment processing |
| Notification Service (`ecommerce-platform-notification-service`) | Manages notifications and messaging |
| UI (`ecommerce-platform-ui`) | React frontend built with Vite |
| Integration Tests (`ecommerce-platform-it`) | Selenium integration tests |

### Infrastructure

- **Nginx** — reverse proxy and rate limiting
- **MySQL** — primary database
- **Kafka** — event streaming for inter-service communication
- **Redis** — caching and session management

## Prerequisites

Before starting, install:

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)

## Quick Start — Development Environment

The development environment uses Docker Compose and supports hot reload for the services.

### 1. Configure environment variables

Review `development/docker-compose.yml` and configure the required values before starting the application. These include:

- `JWT_SECRET` — secret key used to generate JWT tokens
- `STRIPE_API_KEY` — Stripe API key for payment processing
- Mail settings for email notifications:
  - `MAIL_HOST`
  - `MAIL_PORT`
  - `MAIL_USERNAME`
  - `MAIL_PASSWORD`

Use your own credentials and keep secrets out of version control. Do not commit real API keys, passwords, or other sensitive values.

### 2. Start the services

From the repository root, run:

```bash
cd development
docker compose up --build
```

Docker Compose will build and start the development services.

### 3. Open the application

When the containers are running, access the application at:

[http://localhost](http://localhost)

### 4. Stop the services

To stop and remove the containers, run this from the `development` directory:

```bash
docker compose down
```

To also remove the volumes (this deletes persisted database data), run:

```bash
docker compose down -v
```

> **Warning:** `docker compose down -v` removes the associated volumes and can delete database data. Use it only when you intend to reset the development environment.

## Development Features

- **Spring Boot DevTools:** automatic reloading for Java services (approximately 8–10 seconds, depending on the change)
- **Vite HMR:** frontend updates without a full page reload
- **Remote debugging:** port `505` is exposed for IDE debugging
- **Volume mounts:** source changes are reflected in the running development environment

For additional development setup details, see [`development/README.md`](development/README.md).

## Selenium Integration Tests

A separate module for Selenium integration tests is located at `ecommerce-platform-it`.

To run the integration tests:

1. Start the development environment using `docker compose up`.
2. Configure `ecommerce-platform-it/src/test/resources/it-test.properties` with the test database connection details, if required by your setup.
3. Run the integration tests using your IDE or Maven.

Example test database properties shown in the project documentation:

```properties
db.url=jdbc:mysql://localhost:3306/ecommerce-platform
db.username=root
db.password=1234
```

> **Warning:** Integration tests may clear existing data in the test database. Use a dedicated test database and do not run them against production or valuable local data.

## Repository Structure

```text
.
├── .github/
├── demo/
├── development/
├── ecommerce-platform-it/
├── ecommerce-platform-notification-service/
├── ecommerce-platform-payment-service/
├── ecommerce-platform-server/
├── ecommerce-platform-ui/
├── .gitignore
├── LICENSE.md
├── pom.xml
└── README.md
```

## Contributing

Issues and pull requests are welcome. Please describe the purpose of a change and include relevant testing details when submitting a pull request.

## License

See [`LICENSE.md`](LICENSE.md) for license information.
