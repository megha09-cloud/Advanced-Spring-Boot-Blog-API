# Spring Boot Real-Time API

A robust and scalable Spring Boot application offering real-time API services with user authentication, post and comment management, and advanced security features. Built with industry best practices, this project is ideal for developers who want a production-ready API backend with a clean and maintainable codebase.

---

-   [Features ✨](#features)
-   [Project Structure 📁](#project-structure)
-   [Getting Started 🏁](#getting-started)
-   [Configuration ⚙️](#configuration)
-   [API Documentation 📖](#api-documentation)
-   [Testing 🧪](#testing)
-   [Deployment 🚀](#deployment)
-   [Contributing 🤝](#contributing)
-   [License 📄](#license)

---

## Features ✨

### User Authentication and Authorization 🔐

-   **JWT-based authentication** for secure stateless sessions.
-   **Role-based access control** with Admin and User roles.
-   Endpoints for **user registration** and **login**.

### Post Management 📝

-   **CRUD operations** for blog posts.
-   **Pagination & sorting** for efficient listing.
-   **Search functionality** to find posts by title or description.

#### AI-Powered Enhancements 🤖

-   **AI-driven content summarization** using locally hosted ollama LLM.

### Comment Management 💬

-   **CRUD operations** for comments.
-   Fetch comments by **post ID**.
-   Ensure comments belong to the correct post.
-   **Role-based permissions** for comment operations.

### User Management 👥

-   **CRUD operations** for user profiles.
-   **Role assignment** for better access control.
-   Retrieve detailed user information.

### Security 🔒

-   **JWT token generation** and validation.
-   Custom user details service for authentication.
-   **Configurable CORS settings** (using environment variables for domain management).
-   **Rate limiting** to prevent abuse of API requests.

### API Documentation 📖

-   **Swagger/OpenAPI integration** for interactive API docs.
-   Detailed annotations and summaries for each endpoint.

### Configuration and Environment Management ⚙️

-   **Externalized configuration** using a `.env` file and environment-specific properties.
-   Easy management of database connections and other settings.

### Exception Handling 🚨

-   Custom exception classes for precise error reporting.
-   Global exception handler to manage API error responses uniformly.

### Database Interaction 🗄️

-   **JPA repositories** for seamless database operations.
-   Entity classes with **Hibernate ORM** for effective object-relational mapping.

### Utility Services 🛠️

-   **ModelMapper** for DTO and entity mapping.
-   **BCrypt** for secure password encoding.

### Testing 🧪

-   **Postman collections** provided for API testing.
-   **Swagger UI** for interactive endpoint testing.

### Deployment and Build 🚀

-   **Docker support** with a Dockerfile and docker-compose configuration.
-   **Maven build configuration** for streamlined project management.

### Logging and Monitoring 📊

-   Configurable logging levels using **SLF4J** with **Logback**.
-   **Actuator endpoints** for health checks and application metrics.

### Industry Best Practices 🏆

-   Clean, maintainable code following design patterns.
-   Well-structured project organization for scalability and readability.

---

## Project Structure 📁

```

app/
├── Dockerfile & docker-compose.yml # Docker support for containerized deployment 🚢
├── pom.xml # Maven build configuration
├── src/
│ ├── main/
│ │ ├── java/ # Application source code
│ │ │ ├── config/ # Configuration classes (security, logging, rate limiting, etc.)
│ │ │ ├── controllers/ # REST controllers (API endpoints)
│ │ │ ├── entities/ # JPA entities mapping to database tables
│ │ │ ├── exceptions/ # Custom exceptions and global error handling
│ │ │ ├── implementations/ # Service implementations
│ │ │ ├── payloads/ # Data Transfer Objects (DTOs)
│ │ │ ├── repositories/ # JPA repository interfaces
│ │ │ ├── security/ # Security components (JWT, authentication filters, etc.)
│ │ │ ├── services/ # Business logic interfaces and implementations
│ │ │ └── utils/ # Utility classes (constants, password encoder, etc.)
│ │ └── resources/ # Application configurations (properties, logback, etc.)
└── .mvn/ # Maven wrapper configuration

```

_Note: The folder structure is simplified for clarity. Each directory contains related files that keep the codebase modular and maintainable._

---

## Getting Started 🏁

### Prerequisites

-   **Java 17** or later
-   **Maven**
-   **Docker** (preferable, for containerized deployment)

### Installation

1. **Clone the repository:**

    ```bash
    git clone https://github.com/Yassinekrn/yassinekrn-real-time-api-spring-boot.git
    cd yassinekrn-real-time-api-spring-boot
    ```

2. **Set up environment variables:**

    Create a `.env` file in the root directory and add the following:

    ```env
    APP_JWT_SECRET=<your_secret_key>
    APP_JWT_EXPIRATION_IN_MS=<duration_in_milliseconds>
    # Uncomment one of the following lines based on your environment
    # OLLAMA_API_URL=http://localhost:11434/api/generate (for local development)
    # OLLAMA_API_URL=http://host.docker.internal:11434/api/generate (for Docker)
    OLLAMA_MODEL_NAME=<model_name>
    CORS_ALLOWED_ORIGINS=https://frontend1.com,https://frontend2.com (must be comma-separated)
    ```

3. **Update `application.properties`:**

    Before building the JAR file, ensure the following configuration is set:

    ```properties
    spring.datasource.url=jdbc:mysql://localhost:3306/blogdb?useSSL=false&serverTimezone=UTC
    ```

    For Docker deployment, comment the above line and use:

    ```properties
    spring.datasource.url=jdbc:mysql://mysql-db:3306/blogdb
    ```

4. **Build the project using Maven:**

    ```bash
    ./mvn clean package
    ```

5. **Build and run Docker containers:**

    ```bash
    docker-compose build --no-cache
    docker-compose down
    docker-compose up -d
    ```

---

## Configuration ⚙️

### Environment Variables and custom configurations

-   **CORS:** Configurable via environment variables to manage allowed domains. (refer to step 2 in the installation section)
-   **Security:** JWT-based authentication is set up with role-based access. (only 2 roles are available by default: `ROLE_USER` and `ROLE_ADMIN`. also, please refer to step 2 in the installation section)
-   **Rate Limiting:** Implemented using Bucket4j to prevent API abuse. (set to 10 requests per minute by default, could be changed in `RateLimitingFilterConfig.java`).

_All configurations are managed via `application.properties` and the `.env` file._
_You can also check the `utils/Constants.java` file for additional configuration constants._

### Note on Admin Role 🛡️

If you want to add the admin role, you will need to manually insert it into the database.

Connect to the database and run the following query:

```sql
INSERT INTO roles(name) VALUES('ROLE_ADMIN');
```

---

## API Documentation 📖

Once the application is running, access the interactive API documentation via:

```
http://localhost:8080/swagger-ui.html
```

This documentation is generated using **Swagger/OpenAPI** and provides comprehensive details for each endpoint.

---

## Testing 🧪

-   **Postman Collection:** Import the provided Postman collection to test all endpoints.
-   **Swagger UI:** Use the interactive Swagger UI for quick API testing and exploration.

---

## Deployment 🚀

-   **Docker:** Use the provided `Dockerfile` and `docker-compose.yml` for containerized deployment.
-   **Maven:** Standard Maven build process is used for project packaging.

---

## Contributing 🤝

Contributions are welcome! Please fork the repository and submit a pull request with your improvements.

---

## License 📄

Distributed under the MIT License. See `LICENSE` for more information.

---


