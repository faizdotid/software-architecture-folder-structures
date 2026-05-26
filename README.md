# Software Architecture Folder Structures

A curated collection of folder structures for various software architectures.
Each structure includes a brief explanation to help you decide when to use it.

---

## Table of Contents

1. [Layered (N-Tier) Architecture](#1-layered-architecture-n-tier)
2. [Monolithic Architecture](#2-monolithic-architecture)
3. [Modular Monolith](#3-modular-monolith)
4. [Microservices Architecture](#4-microservices-architecture)
5. [Hexagonal Architecture (Ports & Adapters)](#5-hexagonal-architecture-ports-and-adapters)
6. [Clean Architecture](#6-clean-architecture)
7. [Domain-Driven Design (DDD)](#7-domain-driven-design-ddd)
8. [Vertical Slice Architecture](#8-vertical-slice-architecture)
9. [CQRS (Command Query Responsibility Segregation)](#9-cqrs)
10. [Event-Driven Architecture](#10-event-driven-architecture)
11. [Component-Based Architecture](#11-component-based-architecture)
12. [Serverless Architecture](#12-serverless-architecture)
13. [Plugin-Based Architecture](#13-plugin-based-architecture)

---

## 1. Layered Architecture (N-Tier)

**When to use:** Small to medium-sized applications where separation of concerns is enough. Great for CRUD apps and prototypes.

```
project/
│
├── cmd/                     # Main entry point (optional)
│   └── main.go
├── presentation/            # API / UI layer
│   ├── controllers/
│   └── views/
├── business/                # Business logic
│   ├── services/
│   └── models/
├── data/                    # Data access
│   ├── repositories/
│   └── migrations/
├── config/
│   └── config.yaml
└── pkg/                     # Shared utilities
```

---

## 2. Monolithic Architecture

**When to use:** Single deployable unit. Good for startups and small teams before splitting into microservices.

```
project/
│
├── cmd/
│   └── main.go
├── api/
│   ├── controllers/
│   └── middlewares/
├── services/                # Business logic
├── models/                  # Domain entities
├── repository/              # Data access
└── config/
```

---

## 3. Modular Monolith

**When to use:** You want the simplicity of a monolith with clear module boundaries. Easier to later extract into microservices.

```
project/
│
├── cmd/
│   └── main.go
├── modules/                 # Bounded modules
│   ├── user/
│   │   ├── handler.go
│   │   ├── service.go
│   │   ├── repository.go
│   │   └── model.go
│   ├── order/
│   │   ├── handler.go
│   │   ├── service.go
│   │   ├── repository.go
│   │   └── model.go
│   └── product/
│       ├── handler.go
│       ├── service.go
│       ├── repository.go
│       └── model.go
├── shared/                  # Common code
│   ├── database/
│   ├── middleware/
│   └── logger/
└── config/
```

---

## 4. Microservices Architecture

**When to use:** Large scale, independent deployability, polyglot persistence, and autonomous teams.

```
project/
│
├── service-user/
│   ├── cmd/
│   ├── api/
│   ├── domain/
│   ├── repository/
│   └── config/
│
├── service-order/
│   ├── cmd/
│   ├── api/
│   ├── domain/
│   ├── repository/
│   └── config/
│
└── shared/
    ├── auth/
    ├── logging/
    └── monitoring/
```

---

## 5. Hexagonal Architecture (Ports and Adapters)

**When to use:** You need to swap external dependencies (DB, messaging, APIs) without touching core logic.

```
project/
│
├── cmd/
│   └── main.go
├── adapters/                # External dependencies
│   ├── api/                 # REST / GraphQL
│   ├── database/
│   └── messaging/
├── core/                    # Business rules
│   ├── domain/
│   ├── services/
│   └── ports/               # Interfaces
└── infrastructure/
    └── config/
```

---

## 6. Clean Architecture

**When to use:** Long-lived projects where testability and dependency direction matter. Core business logic has zero external dependencies.

```
project/
│
├── cmd/
│   └── main.go
├── entities/                # Enterprise-wide business rules
├── usecases/                # Application-specific logic
├── interfaces/              # Adapters (controllers, presenters)
│   ├── api/
│   └── repository/
├── infrastructure/          # DB, web frameworks, logging
│   ├── database/
│   └── logging/
└── config/
```

---

## 7. Domain-Driven Design (DDD)

**When to use:** Complex business domains where modeling real-world concepts (aggregates, entities, value objects) reduces complexity.

```
project/
│
├── cmd/
│   └── main.go
├── domain/                  # Core domain
│   ├── user/
│   │   ├── entity.go
│   │   ├── value_object.go
│   │   ├── aggregate.go
│   │   └── repository.go    # Interface only
│   └── order/
│       ├── entity.go
│       ├── value_object.go
│       ├── aggregate.go
│       └── repository.go
├── application/             # Use cases / services
│   ├── user_service.go
│   └── order_service.go
├── infrastructure/          # Implementation details
│   ├── persistence/
│   │   ├── user_repository.go
│   │   └── order_repository.go
│   └── messaging/
├── interfaces/              # Delivery mechanisms
│   ├── http/
│   └── grpc/
└── config/
```

---

## 8. Vertical Slice Architecture

**When to use:** Features change independently and you want each feature to be self-contained (handler + logic + data access in one slice).

```
project/
│
├── cmd/
│   └── main.go
├── features/                # One folder per feature
│   ├── createUser/
│   │   ├── handler.go
│   │   ├── command.go
│   │   └── validator.go
│   ├── getUser/
│   │   ├── handler.go
│   │   ├── query.go
│   │   └── validator.go
│   └── deleteUser/
│       ├── handler.go
│       ├── command.go
│       └── validator.go
├── shared/                  # Cross-cutting concerns
│   ├── database/
│   ├── middleware/
│   └── logger/
└── config/
```

---

## 9. CQRS

**When to use:** Read and write workloads differ significantly. Reads need optimization (projections, caching) while writes enforce business rules.

```
project/
│
├── cmd/
│   ├── api/                 # Write API
│   └── worker/              # Read projections
├── commands/                # Write side
│   ├── handlers/
│   ├── validators/
│   └── events/
├── queries/                 # Read side
│   ├── handlers/
│   ├── projections/
│   └── dto/
├── domain/
│   ├── aggregates/
│   └── events/
├── infrastructure/
│   ├── read_db/
│   └── write_db/
└── config/
```

---

## 10. Event-Driven Architecture

**When to use:** Systems with high decoupling requirements, real-time processing, or async workflows.

```
project/
│
├── cmd/
│   └── main.go
├── events/
│   └── user_event.go
├── handlers/
│   └── user_event_handler.go
├── services/
├── consumers/               # Kafka, RabbitMQ, etc.
├── producers/
└── config/
```

---

## 11. Component-Based Architecture

**When to use:** Frontend projects or systems built from reusable, interchangeable components.

```
project/
│
├── components/
│   ├── auth/
│   ├── user/
│   └── order/
├── shared/
└── config/
```

---

## 12. Serverless Architecture

**When to use:** Event-triggered, auto-scaling workloads. Pay-per-execution models (AWS Lambda, Azure Functions, Cloudflare Workers).

```
project/
│
├── functions/
│   ├── createUser/
│   ├── processOrder/
│   └── notifyUser/
├── events/
├── models/
├── services/
└── config/
```

---

## 13. Plugin-Based Architecture

**When to use:** Applications that need to be extended by third-party developers or dynamically loaded modules.

```
project/
│
├── core/
│   ├── api/
│   ├── services/
│   └── models/
├── plugins/
│   ├── auth/
│   ├── payments/
│   └── analytics/
├── shared/
└── config/
```

---

## How to Choose

| Architecture | Team Size | Complexity | Scalability | When to Use |
|-------------|-----------|------------|-------------|-------------|
| Layered | Small | Low | Low | CRUD apps, prototypes |
| Monolith | Small-Medium | Low-Medium | Medium | MVPs, small teams |
| Modular Monolith | Medium | Medium | Medium | Pre-microservices stage |
| Microservices | Large | High | High | Independent scaling, polyglot |
| Hexagonal | Medium | Medium | Medium | Swappable dependencies |
| Clean | Medium | Medium | Medium | Long-term maintainability |
| DDD | Medium-Large | High | Medium | Complex business domains |
| Vertical Slice | Medium | Medium | Medium | Feature-centric teams |
| CQRS | Medium-Large | High | High | Different read/write loads |
| Event-Driven | Medium-Large | High | High | Async, decoupled systems |
| Component | Any | Low | Low | Reusable UI/modules |
| Serverless | Small-Medium | Low | Auto | Event-triggered workloads |
| Plugin | Medium | Medium | Medium | Extensible platforms |

---

> These structures are starting points. Adapt them to your team's needs, tech stack, and project scale.
