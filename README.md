# 🟢 Node Telemetry API

> Modern Node.js API layer for fleet telemetry data — the companion API for [fleet-telemetry-platform](https://github.com/YOUR_USERNAME/fleet-telemetry-platform).

[![Node](https://img.shields.io/badge/Node-20+-green)](https://nodejs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-blue)](https://www.typescriptlang.org/)
[![Docker](https://img.shields.io/badge/Docker-ready-blue)](https://www.docker.com/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

---

## 📖 About

This project is the **API/BFF layer** that sits in front of a fleet telemetry data platform. It demonstrates modern Node.js backend patterns: REST + GraphQL APIs, real-time WebSockets, authentication, rate limiting, caching, and production-grade observability.

**Why a separate Node.js project?**
In a realistic data platform, the data engineering side (Python, Spark, Airflow) is separate from the API that users and dashboards consume. This project shows that I can build both — a Python data platform AND a TypeScript API that exposes its data cleanly.

## 🎯 What This Project Demonstrates

- ✅ Clean architecture (controller → service → repository)
- ✅ Dependency injection patterns
- ✅ Type-safe REST + GraphQL APIs
- ✅ Real-time updates via WebSockets
- ✅ JWT authentication with refresh tokens
- ✅ Rate limiting, caching, circuit breakers
- ✅ Observability (structured logs, traces, metrics)
- ✅ Test-driven development (unit + integration)
- ✅ Dockerized development environment
- ✅ CI/CD with GitHub Actions

## 🧰 Tech Stack

**Language:** TypeScript 5
**Runtime:** Node.js 20 LTS
**Framework:** Express → NestJS (migration project)
**Database:** PostgreSQL + Prisma ORM
**Cache:** Redis
**Real-time:** Socket.io
**Queue:** BullMQ
**GraphQL:** Apollo Server
**Testing:** Jest + Supertest
**Validation:** Zod
**Logging:** Pino
**Tracing:** OpenTelemetry
**Containers:** Docker + Docker Compose

## 📂 Repository Structure

```
node-telemetry-api/
├── README.md
├── src/
│   ├── modules/
│   │   ├── vehicles/             # Vehicle domain
│   │   │   ├── controllers/
│   │   │   ├── services/
│   │   │   ├── repositories/
│   │   │   ├── dto/
│   │   │   └── vehicles.module.ts
│   │   ├── telemetry/            # Telemetry domain
│   │   ├── alerts/               # Real-time alerts (WebSockets)
│   │   └── auth/                 # Authentication
│   ├── shared/
│   │   ├── middlewares/
│   │   ├── errors/
│   │   └── utils/
│   ├── infrastructure/
│   │   ├── database/             # Prisma setup
│   │   ├── cache/                # Redis client
│   │   ├── queue/                # BullMQ workers
│   │   └── observability/        # OpenTelemetry setup
│   ├── graphql/                  # GraphQL schema + resolvers
│   └── main.ts
├── prisma/
│   ├── schema.prisma
│   └── migrations/
├── tests/
│   ├── unit/
│   └── integration/
├── docker/
│   └── docker-compose.yml
├── .github/workflows/
└── package.json
```

## 🗓️ Implementation Roadmap (16 weeks, every Wednesday)

This project runs in parallel with the data platform, using the Wednesday slot dedicated to Node.js in my study plan.

### Phase 1 — Foundation (Weeks 1-4)

- [ ] **Week 1:** Project setup — TypeScript, ESLint, Prettier, Husky
- [ ] **Week 2:** Express server with layered architecture
- [ ] **Week 3:** Prisma + PostgreSQL, first CRUD (Vehicles)
- [ ] **Week 4:** Input validation with Zod, proper error handling

**Deliverable:** Basic vehicle management API with clean structure.

### Phase 2 — Real Features (Weeks 5-8)

- [ ] **Week 5:** JWT authentication + refresh tokens
- [ ] **Week 6:** RBAC (Role-Based Access Control)
- [ ] **Week 7:** Telemetry endpoints + pagination
- [ ] **Week 8:** WebSocket integration for real-time alerts

**Deliverable:** Production-style auth and real-time features.

### Phase 3 — Advanced Patterns (Weeks 9-12)

- [ ] **Week 9:** Redis caching layer (with invalidation strategies)
- [ ] **Week 10:** Rate limiting + circuit breakers
- [ ] **Week 11:** BullMQ job queues for async processing
- [ ] **Week 12:** GraphQL API as alternative to REST

**Deliverable:** Robust, scalable API patterns.

### Phase 4 — Production Readiness (Weeks 13-16)

- [ ] **Week 13:** Comprehensive testing (unit + integration)
- [ ] **Week 14:** Pino structured logging + OpenTelemetry tracing
- [ ] **Week 15:** Dockerization + multi-stage builds
- [ ] **Week 16:** CI/CD with GitHub Actions + automated deploys

**Deliverable:** Fully production-ready API.

## 🔌 API Endpoints (Preview)

### REST API

```
GET    /api/v1/vehicles              # List fleet vehicles
GET    /api/v1/vehicles/:id          # Get vehicle details
POST   /api/v1/vehicles              # Register new vehicle
PATCH  /api/v1/vehicles/:id          # Update vehicle
DELETE /api/v1/vehicles/:id          # Deactivate vehicle

GET    /api/v1/telemetry/:vehicleId  # Historical telemetry
GET    /api/v1/telemetry/latest      # Real-time positions

GET    /api/v1/alerts                # Active alerts
POST   /api/v1/alerts/acknowledge    # Acknowledge alert

POST   /api/v1/auth/login
POST   /api/v1/auth/refresh
POST   /api/v1/auth/logout
```

### WebSocket Events

```
vehicle:position-updated    # Real-time GPS updates
alert:triggered             # New alert fired
alert:resolved              # Alert resolved
```

### GraphQL (optional, Phase 3)

```graphql
type Vehicle {
  id: ID!
  plate: String!
  model: String!
  currentPosition: Position
  telemetry(from: DateTime, to: DateTime): [TelemetryPoint!]!
}

type Query {
  vehicles(filter: VehicleFilter): [Vehicle!]!
  vehicle(id: ID!): Vehicle
}
```

## 🚀 Getting Started

```bash
# Clone
git clone https://github.com/YOUR_USERNAME/node-telemetry-api.git
cd node-telemetry-api

# Install dependencies
npm install

# Start Docker services (PostgreSQL, Redis)
docker-compose up -d

# Run migrations
npx prisma migrate dev

# Seed database
npm run seed

# Start dev server
npm run dev

# Run tests
npm test
```

## 🎓 Architecture Decisions

Key decisions documented as ADRs in `docs/decisions/`:

- ADR-001: Why Express → NestJS migration in Phase 2
- ADR-002: REST vs GraphQL (why both)
- ADR-003: Prisma vs TypeORM
- ADR-004: Authentication strategy (JWT vs sessions)
- ADR-005: Caching strategy (cache-aside vs write-through)

## 📈 Current Status

**Current phase:** Phase 1 — Foundation
**Last updated:** [UPDATE WEEKLY]

## 🔗 Related Projects

- [fleet-telemetry-platform](https://github.com/YOUR_USERNAME/fleet-telemetry-platform) — The data engineering backend this API consumes
- [ml-anomaly-pipeline](https://github.com/YOUR_USERNAME/ml-anomaly-pipeline) — ML pipeline feeding anomaly alerts back into this API

## 👤 Author

**Kaike Oliveira** — Software Engineer with production experience in distributed systems, IoT, and real-time data.

- 💼 LinkedIn: [linkedin.com/in/kaikeoliveira](https://www.linkedin.com/in/kaikeoliveira)

## 📝 License

MIT
