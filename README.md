# Nexus B2B Defect Triage Platform

## Project Overview
Nexus is a robust, intermediate-level B2B web application designed to log, track, and triage manufacturing and structural defects. Built with a focus on backend scalability, it features role-based access control (RBAC), memory-efficient data streaming for high-volume logs, and a clean, minimalist frontend for operational dashboards.

## Tech Stack
*   **Backend:** Node.js (v20+), Express.js (v4)
*   **Database:** PostgreSQL (v16) with Prisma ORM (for type-safe database access and migration management)
*   **Frontend:** React 18 (Vite), Zustand (State Management), TailwindCSS (Minimalist UI)
*   **Security:** JSON Web Tokens (JWT), bcryptjs, Helmet, Express Rate Limit
*   **Testing:** Jest, Supertest (Backend Integration)
*   **DevOps:** Docker, GitHub Actions (CI/CD)

## Development Roadmap

### Phase 1: Database Design & Core Infrastructure
*   [ ] Initialize Node.js environment and configure TypeScript (optional but recommended for enterprise scale).
*   [ ] Setup PostgreSQL database (local or via Docker).
*   [ ] Define Prisma schema with relational modeling:
    *   `Tenant` (B2B clients)
    *   `User` (Admin, Inspector, Analyst roles)
    *   `Defect` (Foreign keys to User and Tenant, with status enums: Open, In-Progress, Resolved).
*   [ ] Implement secure environment variable management using `dotenv`.

### Phase 2: Authentication & Security Protocols
*   [ ] Develop Auth middleware validating JWT access tokens.
*   [ ] Implement password hashing using `bcryptjs` before DB insertion.
*   [ ] Apply Express middlewares: `helmet` for HTTP headers, `cors` for origin restriction, and `express-rate-limit` to prevent brute-force attacks on login routes.
*   [ ] Centralize error handling to prevent stack trace leaks in production.

### Phase 3: Robust API Design (The Service Layer)
*   [ ] Build RESTful CRUD endpoints for `Users` and `Defects`.
*   [ ] Implement an asynchronous, generator-based streaming endpoint to handle massive volumes of synthetic or historical defect log data without overloading server RAM.
*   [ ] Implement pagination, filtering, and sorting at the database query level to optimize payload sizes.

### Phase 4: Frontend Integration (Minimalist Dashboard)
*   [ ] Scaffold React app using Vite for optimized build times.
*   [ ] Configure Axios instances with request/response interceptors to automatically attach JWTs and handle 401 Unauthorized token refreshes.
*   [ ] Implement global state using Zustand to manage user sessions and active triage filters.
*   [ ] Build a minimalist dashboard utilizing TailwindCSS to render defect data in clean, highly readable tables.

### Phase 5: DevOps & Automated Testing
*   [ ] Write unit and integration tests using Jest and Supertest, targeting the authentication flow and core CRUD logic.
*   [ ] Containerize the application using a `docker-compose.yml` file to orchestrate the Node server, React client, and Postgres database.
*   [ ] Create a GitHub Actions workflow to run the test suite automatically on Pull Requests to the `main` branch.