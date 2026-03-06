*This project has been created as part of the 42 curriculum by hchin, gihokim, yuna, seongkim, djang.*

# ft_transcendence

A real-time multiplayer web gaming platform built as the final project of the 42 Common Core. Users can register, manage profiles, add friends, create or join game rooms, chat in real-time, and compete against each other through WebSocket-powered live matches.

---

## Table of Contents

- [Description](#description)
- [Team Information](#team-information)
- [Project Management](#project-management)
- [Technical Stack](#technical-stack)
- [Database Schema](#database-schema)
- [Features List](#features-list)
- [Modules](#modules)
- [Individual Contributions](#individual-contributions)
- [Instructions](#instructions)
- [Resources](#resources)

---

## Description

**ft_transcendence** is a full-stack web application that provides a real-time multiplayer gaming platform. The project features a responsive React frontend, a Fastify-powered RESTful backend, MariaDB for data persistence, and WebSocket integration for live game interaction and chat.

### Key Features

- User registration and JWT-based authentication
- User profile management with avatar upload
- Friend system (add, accept, reject, block)
- Real-time game lobby and match rooms
- WebSocket-powered live chat and game synchronization
- User presence (online/offline status)
- Privacy Policy and Terms of Service pages
- Swagger/OpenAPI interactive documentation
- HTTPS via Caddy reverse proxy with self-signed certificates
- Fully containerized with Docker Compose

---

## Team Information

| Member | Login | Role(s) | Responsibilities |
|--------|-------|---------|-----------------|
| Kim Gihong | gihokim | PO | Backend development & database design |
| Kim Seongju | seongkim | PM | Frontend development & infrastructure setup |
| Jang Jaehyuk | djang | TL | Frontend development & dev lead |
| Jin Hyungbin | hchin | - | Frontend development & documentation |
| Na Yumin | yuna | - | Real-time communication development & testing |

> **Roles:** Product Owner (PO), Project Manager (PM), Technical Lead / Architect, Developers (all members)

---

## Project Management

- **Task Distribution:**
Tasks are first categorized by domain (Frontend / Backend / WebSocket / DevOps, etc.), then broken down into issue-level subtasks with assigned owners.
Each feature has a single responsible owner, while critical logic (game logic, authentication, socket communication, etc.) is designed collaboratively by two or more members.
When urgent bugs arise, priorities are reassigned and all members participate in resolution.
- **Project Management Tools:**
GitHub Issues is the central tool for managing features and bugs.
Issues are classified using labels such as `feature`, `fix`, `refactor`, and `docs`, with Milestones used to set sprint-level goals.
All PRs are linked to their related Issues.
- **Communication Channels:**
**Discord:** Used for real-time technical discussions, screen sharing, announcements, and recording key decisions.
**KakaoTalk:** Used for urgent communication and schedule coordination.
- **Meeting Cadence:**
Weekly regular meetings are held to share feature progress and set goals for the next sprint.
Ad-hoc small meetings are held as needed per feature, and full-team meetings are required for major architectural changes.
- **Code Reviews:**
All code is merged via Pull Requests, requiring at least one approval before merge.
Logic changes, game state management, and WebSocket handling are recommended for review by two or more members.
Reviews check for proper error handling, memory/state management adequacy, type safety, and impact on existing features.
- **Branch Strategy:**
Each member works on their own branch using the `<nickname>/<scope>` naming convention (e.g., `yuna/websocket`, `gihokim/auth`).
The `main` branch is always kept in a deployable state. Features are merged into `main` via PR after development. Direct pushes to `main` are prohibited.

### Commit Convention

```
<type>[optional scope]: <description>
```

| Type | Description |
|------|-------------|
| feat | New feature |
| fix | Bug fix |
| docs | Documentation changes |
| style | Code formatting (no logic changes) |
| refactor | Code refactoring (no feature changes) |
| test | Adding or modifying tests |
| chore | Build tasks, package manager config, etc. |

---

## Technical Stack

### Frontend

| Technology | Purpose |
|-----------|---------|
| **React 19** | UI framework |
| **TypeScript** | Type-safe development |
| **Vite** | Build tool and dev server |
| **React Router DOM** | Client-side routing |
| **styled-components** | Component-scoped CSS-in-JS styling |
| **react-cookie** | Cookie-based token management |

### Backend

| Technology | Purpose |
|-----------|---------|
| **Fastify** | High-performance Node.js web framework |
| **TypeScript** | Type-safe development |
| **Prisma ORM** | Database access and migrations |
| **@fastify/jwt** | JWT-based authentication |
| **@fastify/websocket** | Real-time WebSocket communication |
| **@fastify/swagger** | API documentation (Swagger UI) |
| **@fastify/rate-limit** | Rate limiting (100 req/min) |
| **@fastify/helmet** | Security HTTP headers |
| **Zod** | Request/response schema validation |
| **bcryptjs** | Password hashing |

### Infrastructure

| Technology | Purpose |
|-----------|---------|
| **Docker & Docker Compose** | Containerization and orchestration |
| **MariaDB 11.2** | Relational database |
| **Caddy** | Reverse proxy, HTTPS (self-signed TLS) |

### Why These Choices?

- **React** was chosen for its large ecosystem and component-based architecture, enabling rapid UI development.
- **Fastify** was selected over Express for its superior performance and built-in plugin system (JWT, WebSocket, Swagger all as first-class plugins).
- **MariaDB** provides MySQL compatibility with better performance and is well-supported by Prisma ORM.
- **Prisma** enables type-safe database queries that integrate seamlessly with TypeScript.
- **Caddy** simplifies HTTPS setup with automatic certificate management and clean reverse proxy configuration.

---

## Database Schema

```
+-----------------+       +------------------+       +-------------------+
|    Users        |       |   Friendships    |       |   GameMatches     |
+-----------------+       +------------------+       +-------------------+
| id          PK  |--+    | id           PK  |       | id            PK  |
| email           |  +--->| userId       FK  |       | gameName          |
| username        |  +--->| friendId     FK  |       | hostId        FK  |--+
| passwordHash    |  |    | status           |       | maxPlayers        |  |
| displayName     |  |    | createdAt        |       | currentPlayers    |  |
| avatarUrl       |  |    | updatedAt        |       | status            |  |
| bio             |  |    +------------------+       | winnerId      FK  |  |
| isOnline        |  |                               | startedAt         |  |
| lastSeen        |  |    +------------------+       | endedAt           |  |
| totalWins       |  |    |  MatchPlayers    |       | durationSeconds   |  |
| totalLosses     |  |    +------------------+       | createdAt         |  |
| totalGames      |  +--->| userId       FK  |       | updatedAt         |  |
| tokenVersion    |  |    | matchId      FK  |------>+-------------------+  |
| createdAt       |  |    | position         |                              |
| updatedAt       |  |    | score            |       Users.id <-------------+
+-----------------+  |    | isWinner         |
                     |    | placement        |
                     +----| createdAt        |
                          | updatedAt        |
                          +------------------+
```

### Relationships

- **Users** 1:N **GameMatches** (as host)
- **Users** 1:N **GameMatches** (as winner)
- **Users** N:N **Users** (through **Friendships**)
- **Users** N:N **GameMatches** (through **MatchPlayers**)

### Friendship Status Values

| Status | Description |
|--------|-------------|
| `PENDING` | Friend request sent, awaiting response |
| `ACCEPTED` | Both users are friends |
| `BLOCKED` | User has been blocked |

### Match Status Values

| Status | Description |
|--------|-------------|
| `WAITING` | Room created, waiting for players |
| `IN_PROGRESS` | Game is currently being played |
| `COMPLETED` | Game has ended normally |
| `CANCELLED` | Game was cancelled |

---

## Features List

| Feature | Description | Member(s) |
|---------|-------------|-----------|
| User Authentication | Registration, JWT login/logout, password hashing with bcrypt | gihokim, seongkim |
| User Profile | View/edit profile, avatar upload, display name, bio | gihokim, seongkim, djang |
| Friend System | Send/accept/reject friend requests, block users, view friend list | djang |
| Game Lobby | Browse, create, and join game rooms | seongkim, djang, hchin |
| Game Room | Real-time multiplayer game interaction via WebSocket | yuna, hchin, djang |
| Real-time Chat | In-room messaging with WebSocket | seongkim, yuna |
| User Presence | Online/offline status tracking, last seen timestamp | djang |
| API Documentation | Swagger UI at `/docs` with full endpoint reference | gihokim |
| Privacy Policy | Accessible privacy policy page | yuna |
| Terms of Service | Accessible terms of service page | yuna |
| File Upload | Avatar image upload with multipart handling | gihokim, seongkim |
| Rate Limiting | 100 requests per minute per client | gihokim |
| HTTPS | Self-signed TLS certificates via Caddy | seongkim, djang |

---

## Modules

### Selected Modules

| # | Category | Module | Type | Points | Member(s) |
|---|----------|--------|------|--------|-----------|
| 1 | Web | Use a frontend and backend framework | Major | 2 | gihokim, seongkim |
| 2 | Web | Real-time features using WebSockets or similar technology | Major | 2 | yuna, seongkim |
| 3 | Web | User interaction features | Major | 2 | hchin, yuna |
| 4 | Web | Public API implementation | Major | 2 | gihokim |
| 5 | Web | Fully web-based game with player-vs-player competition | Major | 2 | djang, yuna, hchin |
| 6 | Web | Remote players support | Major | 2 | djang, hchin, yuna |
| 7 | Web | Multiplayer game (3+ players) | Major | 2 | djang, yuna, hchin |
| 8 | Web | Use an ORM for the database | Minor | 1 | gihokim |

### Point Calculation

| Type | Count | Points Each | Subtotal |
|------|-------|-------------|----------|
| Major modules | 7 | 2 | 14 |
| Minor modules | 1 | 1 | 1 |
| **Total** | | | **15** |

> **Note:** 14 points minimum required. Aim for more in case some modules aren't validated during evaluation.

### Module Justification

Below are the rationale, technical implementation, and assigned members for each module.

#### 1. Use a Frontend and Backend Framework (Major)
- **Justification:** Adopting modern web frameworks was essential for the project's scalability and maintainability, warranting its selection as a Major module.
- **Implementation:**
  - **FE:** Built a component-based architecture using React 19 and TypeScript, with CSS-in-JS styling via Styled-components.
  - **BE:** Leveraged Fastify for superior asynchronous performance and integrated JWT and Swagger through its plugin system.
- **Members:** `gihokim`, `seongkim`

#### 2. Real-time Features Using WebSockets (Major)
- **Justification:** Real-time competitive gameplay and chat are the core of this project, requiring low-latency bidirectional communication, making this a Major module.
- **Implementation:** Built the game server using `@fastify/websocket`. Implemented room-based broadcasting logic to synchronize real-time game state (stone positions) and chat messages.
- **Members:** `yuna`, `seongkim`

#### 3. User Interaction Features (Major)
- **Justification:** Enhancing the social elements of the service required a friend system and real-time status tracking, which constitute a key part of the user experience.
- **Implementation:** Implemented friend request/accept/block functionality via REST API, and reflected users' online/offline status in real-time through WebSocket connection state.
- **Members:** `hchin`, `yuna`

#### 4. Public API Implementation (Major)
- **Justification:** Providing a standardized interface was deemed important for developer-friendliness and system transparency.
- **Implementation:** Integrated `@fastify/swagger` and `@fastify/swagger-ui` to serve interactive API documentation based on OpenAPI Spec 3.0 at the `/docs` endpoint. All endpoints are validated through Zod schemas.
- **Members:** `gihokim`

#### 5. Fully Web-based Game with Player-vs-Player Competition (Major)
- **Justification:** Completing the project's identity as a "gaming platform" required a self-contained game loop within the browser.
- **Implementation:** Rendered graphics using the HTML5 Canvas API, with server-side game engine performing physics calculations to maintain synchronization between clients.
- **Members:** `djang`, `yuna`, `hchin`

#### 6. Remote Players Support (Major)
- **Justification:** Building infrastructure that allows multiple users to connect over a real network beyond the local environment is an essential step for a web service.
- **Implementation:** Containerized all services with Docker Compose and configured Caddy reverse proxy to establish an HTTPS (TLS) environment, enabling secure external access for gameplay.
- **Members:** `djang`, `hchin`, `yuna`

#### 7. Multiplayer Game (3+ Players) (Major)
- **Justification:** Going beyond simple 1v1 matches requires more complex network synchronization and room management logic, making this a technically challenging Major module.
- **Implementation:** Designed a room-based WebSocket architecture with no player limit. Applied optimized broadcasting logic so that multiple players and spectators can participate in the same game session and receive shared data.
- **Members:** `djang`, `yuna`, `hchin`

#### 8. Use an ORM for the Database (Minor)
- **Justification:** A DB management tool was needed for improved productivity and type safety. As a supplementary technical element, it was selected as a Minor module.
- **Implementation:** Abstracted MariaDB interactions using Prisma ORM. Defined the DB structure through schema files and prevented query errors through auto-generated TypeScript types.
- **Members:** `gihokim`

---

## Individual Contributions

### gihokim (Kim Gihong) — PO / Backend Development & Database Design

- **Backend API Design & Implementation:** Designed and built the RESTful API server using Fastify, implementing core endpoints for user authentication (registration, login, logout), user profile management, friend system, and game match management.
- **Database Schema Design:** Designed the Users, Friendships, GameMatches, and MatchPlayers table structures on MariaDB, and established a type-safe data access layer using Prisma ORM.
- **Authentication System:** Designed the JWT-based authentication flow, implemented password hashing with bcryptjs, and built logout handling through token version management.
- **API Documentation:** Configured automatic Swagger UI-based interactive API documentation generation using @fastify/swagger.
- **Product Owner Role:** Defined project requirements, prioritized features, and led the overall backend architecture direction.
- **Challenges & Solutions:** Encountered compatibility issues during migration as Prisma ORM did not fully support certain MariaDB features; resolved by adjusting the schema design and supplementing with Prisma's raw query capabilities. Additionally, implementing immediate logout was difficult due to JWT's stateless nature, which was solved by introducing a token version management mechanism.

### seongkim (Kim Seongju) — PM / Frontend Development & Infrastructure Setup

- **Frontend UI Development:** Built user interface components using React 19 and TypeScript, applying component-scoped styling with styled-components.
- **Infrastructure Configuration:** Containerized all services (frontend, backend, database, reverse proxy) using Docker Compose, with separate configurations for development and production environments.
- **Caddy Reverse Proxy Setup:** Configured HTTPS communication with self-signed TLS certificates and set up reverse proxy routing for frontend and backend API requests.
- **Build Automation:** Created a Makefile to automate build, run, stop, and cleanup tasks with convenient commands.
- **Project Manager Role:** Managed the overall project schedule, coordinated task distribution among team members, and tracked project progress.
- **Challenges & Solutions:** Faced difficulties separating development and production environments due to complex network communication settings between the frontend hot-reload server and the backend in Docker Compose; resolved by adopting multi-stage builds and splitting Compose files per environment. Also encountered browser security policy conflicts when configuring Caddy's self-signed certificates, which were resolved by adjusting TLS settings and reverse proxy routing rules.

### djang (Jang Jaehyuk) — TL / Frontend Development & Dev Lead

- **Frontend Architecture Design:** Designed the React component structure and established client-side routing using React Router DOM.
- **Game Lobby & Match Room UI:** Developed the frontend interface for game room creation, joining, and browsing, and implemented dynamic UI reflecting real-time game state.
- **State Management & Data Flow Design:** Designed state management patterns across the frontend, and implemented JWT token management and authentication state persistence using react-cookie.
- **Code Quality Management:** Defined team-wide code conventions, led code reviews, and established branch strategy (`<nickname>/<scope>`) and commit conventions.
- **Technical Lead Role:** Led technical decision-making, coordinated the interface between frontend and backend, and helped team members resolve technical challenges.
- **Challenges & Solutions:** Prop drilling across React components became increasingly difficult to maintain as the application grew; resolved by introducing appropriate state management patterns and redesigning the component structure. Also faced challenges balancing real-time state changes with rendering performance in the game room UI, which were addressed by applying optimization techniques to reduce unnecessary re-renders.

### hchin (Jin Hyungbin) — Frontend Development & Documentation

- **Frontend Page Implementation:** Developed frontend pages including user profile, privacy policy, and terms of service as React components.
- **User Profile Features:** Implemented frontend functionality for profile viewing and editing, avatar image upload, display name and bio editing.
- **Friend System UI:** Developed the frontend interface for sending, accepting, and rejecting friend requests, blocking users, and viewing the friend list.
- **Project Documentation:** Authored project documentation including README files (Korean/English) and API docs, and organized and documented team members' contributions.
- **Challenges & Solutions:** Managing real-time presence status updates and friend request state synchronization in the friend system UI led to UI state desynchronization issues; resolved by designing a state management logic that combines WebSocket events with REST API responses.

### yuna (Na Yumin) — Real-time Communication Development & Testing

- **WebSocket Communication:** Implemented server-side WebSocket handlers using @fastify/websocket and developed client-side service modules for managing WebSocket connections.
- **Real-time Chat Feature:** Built real-time message sending and receiving within game rooms, and developed message broadcasting logic through WebSocket.
- **Real-time Game Synchronization:** Implemented real-time game state synchronization via WebSocket to ensure smooth multiplayer gameplay.
- **User Presence Management:** Tracked user online/offline status based on WebSocket connection state and implemented last seen timestamp updates.
- **Testing:** Conducted integration testing across all features and verified the stability of WebSocket connection teardown and reconnection logic.
- **Challenges & Solutions:** WebSocket message ordering and disconnection handling became unstable under concurrent multi-client connections; resolved by implementing room-level message queuing and heartbeat-based connection health detection. Game state synchronization suffered from screen inconsistencies due to network latency, which was addressed by adopting a server-authoritative model.

---

## Instructions

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/) (v20.10+)
- [Docker Compose](https://docs.docker.com/compose/install/) (v2.0+)
- [Make](https://www.gnu.org/software/make/)

### Setup

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd ft_transcendence
   ```

2. **Create the environment file:**
   ```bash
   cp .env.example .env
   ```

3. **Edit `.env`** and set secure values:
   - `MARIADB_ROOT_PASSWORD` - database root password
   - `MARIADB_PASSWORD` - database user password
   - `JWT_SECRET` - a strong secret key for JWT token signing

4. **Build and run (production):**
   ```bash
   make prov
   make up
   ```

   Or for development:
   ```bash
   make dev
   make up
   ```

5. **Access the application:**
   - Frontend: `https://localhost`
   - API Documentation (Swagger): `https://localhost/docs`
   - Health Check: `https://localhost/health`

   > Since the project uses self-signed certificates, your browser will show a security warning. Accept the risk to proceed.

### Useful Commands

| Command | Description |
|---------|-------------|
| `make up` | Start all services |
| `make down` | Stop all services |
| `make re` | Rebuild and restart |
| `make logs` | View container logs |
| `make clean` | Remove containers and volumes |
| `make help` | Show available commands |

### API Endpoints Overview

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/register` | Register a new user |
| POST | `/api/auth/login` | Login and receive JWT token |
| POST | `/api/auth/logout` | Logout and invalidate token |
| GET | `/api/users/me` | Get current user profile |
| PUT | `/api/users/me` | Update current user profile |
| GET | `/api/users/:id` | Get user by ID |
| POST | `/api/friends/request` | Send a friend request |
| PUT | `/api/friends/:id/accept` | Accept a friend request |
| PUT | `/api/friends/:id/reject` | Reject a friend request |
| DELETE | `/api/friends/:id` | Remove a friend |
| PUT | `/api/friends/:id/block` | Block a user |
| GET | `/api/friends` | List all friends |
| POST | `/api/matches` | Create a new game room |
| GET | `/api/matches` | List active matches |
| GET | `/api/matches/:id` | Get match details |
| POST | `/api/matches/:id/join` | Join a match |
| POST | `/api/matches/:id/leave` | Leave a match |
| POST | `/api/matches/:id/start` | Start a match (host only) |
| WS | `/ws/:roomId` | WebSocket for game room |

> For full API documentation with request/response examples, see [API.md](API.md) or visit `/docs` (Swagger UI) when the server is running.

---

## Resources

### Documentation and References

- [React Documentation](https://react.dev/)
- [Fastify Documentation](https://fastify.dev/docs/latest/)
- [Prisma Documentation](https://www.prisma.io/docs)
- [MariaDB Documentation](https://mariadb.com/kb/en/documentation/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [Caddy Documentation](https://caddyserver.com/docs/)
- [WebSocket API (MDN)](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket)
- [styled-components Documentation](https://styled-components.com/docs)
- [Zod Documentation](https://zod.dev/)
- [JWT Introduction](https://jwt.io/introduction)

### AI Usage

AI tools were utilized throughout the development process to improve efficiency.

- **Tools Used:** Claude (Anthropic), Gemini (Google DeepMind)
- **Scope of Work:**
  - **Boilerplate & Structure Design:** Used for initial Fastify server plugin configuration, Prisma schema design, and generating base React component structures.
  - **Debugging & Problem Solving:** Used to analyze and devise solutions for various configuration and runtime errors, including Makefile syntax errors, Docker Compose volume mount issues, and TypeScript type errors.
  - **Documentation:** Automated drafting of README and technical documentation, and documentation of complex API specifications to improve accuracy.
  - **Code Refactoring:** Contributed to optimizing repetitive logic and consistently adjusting code style to match project conventions.
- **Review & Validation Process:**
  - All AI-suggested code was executed and tested by team members in their local environments to verify correct functionality.
  - Security-critical authentication logic (JWT) and database access layers were rigorously reviewed through manual code review to ensure compliance with project requirements before final integration.
  - Build tools and infrastructure configurations were validated through integration testing before and after deployment to ensure system stability.

---

## License

This project was developed as part of the 42 school curriculum. All rights reserved.
