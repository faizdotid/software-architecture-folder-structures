# Folder Structures for Different Software Architectures

Below are examples of folder structures for various software architectures.

## 1. Layered Architecture (N-Tier Architecture)

```
project/
│
├── cmd/                     # Main entry point (optional for larger projects)
│   └── main.go
├── presentation/            # Presentation layer (API, UI)
│   ├── controllers/         # Handlers for requests
│   └── views/               # HTML, Templates (for UI)
├── business/                # Business logic layer
│   ├── services/            # Core business logic
│   └── models/              # Domain models/entities
├── data/                    # Data access layer
│   ├── repositories/        # Interactions with the database
│   └── migrations/          # Database migrations
├── config/                  # Configuration files
│   └── config.yaml
└── pkg/                     # Shared utilities or packages
```

## 2. Microservices Architecture

```
project/
│
├── service-user/            # User service
│   ├── cmd/                 # Main entry point
│   ├── api/                 # API endpoints
│   ├── domain/              # Business logic for user
│   ├── repository/          # Data access for user service
│   └── config/              # Configuration for user service
│
├── service-order/           # Order service
│   ├── cmd/                 # Main entry point
│   ├── api/                 # API endpoints
│   ├── domain/              # Business logic for order
│   ├── repository/          # Data access for order service
│   └── config/              # Configuration for order service
│
└── common/                  # Shared components (auth, logging, etc.)
    ├── auth/
    ├── logging/
    └── monitoring/
```

## 3. Hexagonal Architecture (Ports and Adapters)

```
project/
│
├── cmd/
│   └── main.go              # Main application entry point
├── adapters/                # External dependencies
│   ├── api/                 # REST API or GraphQL interfaces
│   ├── database/            # Database connections
│   └── messaging/           # Message queues or event systems
├── core/                    # Core domain logic (business rules)
│   ├── domain/              # Entities, aggregates, value objects
│   ├── services/            # Application services
│   └── ports/               # Interfaces for external systems
└── infrastructure/          # Frameworks and drivers
    └── config/              # Configuration and setup
```

## 4. Clean Architecture

```
project/
│
├── cmd/                     # Main application entry point
│   └── main.go
├── entities/                # Core domain entities
│   └── user.go
├── usecases/                # Use case (application) layer
│   └── user_usecase.go      # Application logic for user-related operations
├── interfaces/              # Interface adapters (controllers, presenters, etc.)
│   ├── api/                 # API controllers
│   └── repository/          # Data access implementations (DB, API)
├── infrastructure/          # Frameworks and drivers (database, logging, etc.)
│   ├── database/            # DB interactions
│   └── logging/             # Logging setup
└── config/                  # Configuration files
```

## 5. Monolithic Architecture

```
project/
│
├── cmd/
│   └── main.go              # Main entry point
├── api/                     # API endpoints
│   ├── controllers/         # Request handlers
│   └── middlewares/         # Middleware for request lifecycle
├── services/                # Business logic and services
├── models/                  # Data models or domain entities
├── repository/              # Data access layer
└── config/                  # Configuration files
```

## 6. Event-Driven Architecture

```
project/
│
├── cmd/                     # Entry points for event processors
│   └── main.go
├── events/                  # Event definitions
│   └── user_event.go
├── handlers/                # Event handlers
│   └── user_event_handler.go
├── services/                # Business logic reacting to events
├── consumers/               # Event consumers (e.g., Kafka, RabbitMQ)
├── producers/               # Event producers
└── config/                  # Configuration for event sources
```

## 7. Component-Based Architecture

```
project/
│
├── components/              # Modular, reusable components
│   ├── auth/                # Authentication component
│   ├── user/                # User management component
│   └── order/               # Order management component
├── shared/                  # Shared utilities or code between components
└── config/                  # Application configuration
```

## 8. Serverless Architecture

```
project/
│
├── functions/               # Individual serverless functions
│   ├── createUser/          # User creation function
│   ├── processOrder/        # Order processing function
│   └── notifyUser/          # Notification function
├── events/                  # Event definitions for triggering functions
├── models/                  # Data models shared between functions
├── services/                # Business logic and reusable services
└── config/                  # Configuration (e.g., for AWS Lambda, Azure Functions)
```

## 9. Plugin-Based Architecture

```
project/
│
├── core/                    # Core application logic
│   ├── api/
│   ├── services/
│   └── models/
├── plugins/                 # Plugins adding modular functionality
│   ├── auth/                # Authentication plugin
│   ├── payments/            # Payment plugin
│   └── analytics/           # Analytics plugin
├── shared/                  # Shared code between core and plugins
└── config/                  # Configuration for core and plugins
```

Each folder structure serves a different purpose depending on the type of project and scale of the application being built. These structures can be modified according to team needs and the technologies used.

## Credits

- [ChatGPT](https://chatgpt.com/)
