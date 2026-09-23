# Claude Code Prompt Pack for Delivery System Development

Набор специализированных промптов для построения курьерского сервиса с AI-интеграцией.

## 1. Phase 1 — Project initialization

```markdown
You are an expert full-stack engineer.
Build a delivery system with:
- React Native apps for client, courier, admin
- NestJS backend
- PostgreSQL + Redis
- FastAPI AI service
- real-time tracking via Socket.IO
- admin dashboard
- Claude MCP integration

Create complete project structure, package files, .env examples, tsconfig, README, Docker files.
```

## 2. Phase 2 — Authentication

```markdown
Create a secure authentication system for a delivery app.
Requirements:
- User roles: client, courier, admin
- JWT + refresh tokens
- bcrypt password hashing
- login/register endpoints
- current user endpoint
- Auth middleware with role restrictions
- React Native auth screens and Zustand store
```

## 3. Phase 3 — Orders, deliveries and routes

```markdown
Create a complete business domain for a delivery service:
- User, Order, Delivery, Route, Rating entities
- CRUD services and controllers
- real-time tracking via Socket.IO
- route assignment logic
- courier availability logic
- mobile screens for client and courier flows
```

## 4. Phase 4 — AI route optimization

```markdown
Build a Python FastAPI AI service for routing.
Requirements:
- Google OR-Tools VRP optimization
- ETA prediction
- dynamic pricing
- demand prediction
- Redis cache
- MCP servers for Claude integration
- backend wrappers for AI calls
```

## 5. Phase 5 — Admin dashboard

```markdown
Create a React + Vite admin dashboard for a courier service.
Features:
- order monitoring
- user management
- analytics charts
- courier performance
- real-time updates
- settings page
```

## 6. Phase 6 — Deployment

```markdown
Prepare a production-ready deployment setup for the delivery system.
Include:
- docker-compose
- Dockerfiles
- GitHub Actions workflows
- environment templates
- monitoring config
- deployment guide
```

---

## 7. Useful follow-up prompt

```markdown
Review the generated code, find bugs, and refactor it with improved architecture, validation, error handling, and production-level quality.
```

---

## 8. Best workflow

For this type of project:
- use Claude Code for architecture and complex logic
- use Codex for tests, boilerplate, repeated code generation
- validate all AI decisions with deterministic business logic
