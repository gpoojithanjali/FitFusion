# FitFusion

A full-featured health and fitness backend system built using Node.js, Express, GraphQL, Sequelize, and MySQL. It supports user tracking, trainer assignments, workout and meal planning, and integrates with external weather data APIs. Includes frontend demonstration, CI/CD pipeline, logging, tests, and Docker containerization.

---

## 📌 Table of Contents

- [Project Overview](#project-overview)
- [System Architecture](#system-architecture)
- [Technology Stack](#technology-stack)
- [Database Design](#database-design)
- [API Design](#api-design)
- [External API Integration](#external-api-integration)
- [Frontend Demonstration](#frontend-demonstration)
- [Testing Strategy](#testing-strategy)
- [Logging Mechanism](#logging-mechanism)
- [CI/CD Pipeline](#cicd-pipeline)
- [Setup Instructions](#setup-instructions)
- [Postman/API Testing](#postmanapi-testing)
- [Deployment](#deployment)
- [Future Improvements](#future-improvements)

---

## 📚 Project Overview

FitFusion is a backend platform enabling fitness tracking and health goal management. Users can log meals, workouts, and goals, and be assigned to trainers. Real-time weather integration enhances outdoor activity planning. The project demonstrates skills in REST/GraphQL APIs, database design, Docker, testing, and DevOps automation.

---

## 🧱 System Architecture

FitFusion follows a modular monolithic architecture built with:

- Express.js for REST API
- GraphQL via graphql-http for flexible querying
- Sequelize ORM for SQL abstraction
- External API utilities
- React frontend as a separate container

![](https://fake-architecture-diagram.com/fitfusion.svg) <!-- Replace with actual image if desired -->

While monolithic, the system is dockerized with separate services for frontend, backend, and database, allowing future migration to microservices if needed.

---

## ⚙️ Technology Stack

| Layer | Tech |
|------|------|
| Backend | Node.js, Express.js |
| API | GraphQL (graphql-http), REST |
| ORM | Sequelize |
| Database | MySQL |
| Frontend | React + Tailwind CSS (Vite) |
| CI/CD | GitHub Actions |
| Containerization | Docker + Docker Compose |
| Testing | Jest |
| Logging | Winston |
| External API | OpenWeatherMap |

---

## 🗄️ Database Design

- Type: SQL (MySQL)
- ORM: Sequelize
- Tables:
  - Users
  - Trainers
  - UserTrainer (many-to-many)
  - Workouts
  - Meals
  - Goals

Diagram:

```mermaid
erDiagram
    USER ||--o{ WORKOUT : has
    USER ||--o{ MEAL : logs
    USER ||--o{ GOAL : tracks
    USER ||--o{ USERTRAINER : assigned
    TRAINER ||--o{ USERTRAINER : trains
```

- ✅ Relational constraints
- ✅ Validation rules (Sequelize)
- ✅ Complex queries supported via GraphQL resolvers

---

## 🧪 API Design

Supports both REST and GraphQL:

### GraphQL

- Endpoint: /graphql
- Playground: /graphiql
- Operations:
  - Create/Update/Delete: users, meals, workouts, goals
  - Query: users with nested goals and trainer info

Example Query:

```graphql
query {
  getUser(id: 1) {
    name
    goals {
      description
      status
    }
  }
}
```

### REST

- Routes:
  - GET/POST /users
  - PUT /goals/:id
  - DELETE /workouts/:id
  - GET /weather?city=Boston

- Validation using Express middleware
- Error-handling middleware for graceful failures

---

## 🌐 External API Integration

- API Used: OpenWeatherMap
- Purpose: Show weather for planning outdoor activities
- Usage:
  - Endpoint: /weather?city=London
  - Handled via utils/weather.js

Frontend displays:
- Temperature
- Condition
- Location

API key stored securely in `.env`

---

## 🖥️ Frontend Demonstration

- SPA built with React + Tailwind CSS
- Pages:
  - Home (summary)
  - Users (create/view/edit)
  - Workouts, Meals, Goals
  - Weather (weather API demo)
- Data fetched using Axios and GraphQL client


---

## ✅ Testing Strategy

- Framework: Jest
- Tests:
  - Unit tests for models (e.g. Meal.test.js)
  - Integration tests for routes and API (e.g. healthcheck, goals)
- Coverage:
  - User creation
  - Goal logging
  - Weather API call mocking

Run tests:

```bash
npm test
```

---

## 📜 Logging Mechanism

- Logger: Winston
- Logging levels: info, error, warn
- Logs to: console + rotating log files
- Sample:

```js
logger.info('User created:', userId);
logger.error('Database connection failed');
```

Location: utils/logger.js

---

## ⚙️ CI/CD Pipeline

- Platform: GitHub Actions
- File: .github/workflows/ci.yml
- Workflow:
  - Lint code
  - Run tests
  - Build Docker containers
  - Trigger deployment

Status badge:

![CI Status](https://github.com/gpoojithanjali/FitFusion/actions/workflows/main.yml/badge.svg)

---

## 🚀 Setup Instructions

### Prerequisites

- Docker & Docker Compose
- Node.js
- MySQL (if not using Docker DB)

### Local Development

1. Clone the repo:

```bash
git clone https://github.com/username/fitfusion.git
cd fitfusion
```

2. Create .env file:

```env
DB_USER=root
DB_PASS=yourpassword
DB_NAME=fitfusion
OPENWEATHER_API_KEY=your_api_key
```

3. Run with Docker:

```bash
docker-compose up --build
```

4. Access:

- Backend: http://localhost:4000
- GraphiQL: http://localhost:4000/graphiql
- Frontend: http://localhost:3000

---

## 📫 Postman/API Testing

- GraphQL examples provided in `/docs/graphql-queries.md`
- Health Check: GET /health

---

## 📦 Deployment

Docker containers deployable via:

```bash
docker-compose -f docker-compose.prod.yml up -d
```

---

## 💡 Future Improvements

- Switch to Microservices using gRPC
- Add authentication/authorization (JWT)
- Notifications via email/SMS
- Real-time tracking via WebSockets
- Admin dashboard
- iOS/Android client

---

## 🎤 Final Presentation Topics

- Architecture Walkthrough
- GraphQL + REST hybrid approach
- Trainer/user many-to-many model
- External API demo (weather)
- DevOps automation (CI/CD)
- Logging + Testing strategy
