# LifeCore

> Your Personal Data Platform - Track your life, health, coding, and productivity in one place. All your data, owned by you.

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

---

## Overview

LifeCore is a web-first personal data platform that unifies your digital life into a single, personal dashboard. Built as a monorepo with a FastAPI backend and Next.js frontend, it provides a foundation for modules that track GitHub activity, workouts, reading, calendar events, system performance, and more.

### What LifeCore Is

- A **personal data platform** - you own and control all your data
- A **web-first architecture** - browser interface with a REST API backend
- A **progressive enhancement system** - start with core, add modules over time
- A **plugin-based architecture** - integrations are independent modules

### What LifeCore Is Not (Yet)

- Not a complete production-ready application (V0.1 is a foundation)
- Not a ready-to-deploy solution (requires local setup)
- Not a mobile app (web interface only for now)
- Not a cloud service (runs on your machine)

---

## Project Vision

The vision for LifeCore is to create a **personal operating system** for your digital life. Imagine having a dashboard that shows:

- Your daily coding activity from GitHub
- Your workout streaks and progress
- Your reading history and page counts
- Your calendar events and meeting load
- Your system performance and resource usage
- Your screen time and productivity ROI

All of this data living in one place, owned entirely by you, with no third-party tracking or data mining.

---

## Current V0.1 Scope

V0.1 is the **walking skeleton** - the foundation upon which everything else is built. This release focuses on:

| Component | Status | Description |
|-----------|--------|-------------|
| API Layer | ✅ Implemented | FastAPI backend with auth, database, and basic endpoints |
| Web Layer | ✅ Implemented | Next.js 14 frontend with pages and routing |
| Database | ✅ Implemented | SQLAlchemy with SQLite (development) |
| Docker | ✅ Implemented | Docker Compose for containerized development |
| Plugin System | ✅ Implemented | Framework for integrations with lifecycle hooks |
| GitHub Integration | ✅ Implemented | Plugin for fetching GitHub commits |
| UI Components | ✅ Implemented | Reusable Button, Card, and layout components |

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                           PERSONAL OS                                │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ┌──────────────┐         ┌──────────────┐         ┌──────────────┐ │
│  │   Web App    │ ←─────> │   FastAPI    │ ←─────> │  PostgreSQL  │ │
│  │  (Next.js)   │   API   │  (Python)    │  Data   │   (Dev:      │ │
│  │              │  Routes │              │  Flow   │   SQLite)    │ │
│  └──────────────┘         └──────────────┘         └──────────────┘ │
│                                      │                               │
│                                      ▼                               │
│                         ┌──────────────────────┐                     │
│                         │   Plugin Framework   │                     │
│                         └──────────────────────┘                     │
│                           │        │        │                        │
│          ┌────────────────┼────────┼────────┼────────┐              │
│          ▼                ▼        ▼        ▼        ▼              │
│    ┌─────────┐    ┌─────────┐  ┌─────────┐  ┌─────────┐   ┌─────────┐│
│    │ GitHub  │    │ Workouts│  │ Reading │  │ Calendar│   │ Screen  ││
│    │ Plugin  │    │ Plugin  │  │ Plugin  │  │ Plugin  │   │ Time    ││
│    └─────────┘    └─────────┘  └─────────┘  └─────────┘   └─────────┘│
│                                                                      │
│                    ┌───────────────┐                                 │
│                    │   Modules     │                                 │
│                    └───────────────┘                                 │
│                           │                                          │
│          ┌──────────────┼──────────────┐                            │
│          ▼              ▼              ▼                            │
│     ┌────────┐    ┌──────────┐    ┌────────┐                        │
│     │  Life  │    │  Machine │    │   Art  │    (Future Phases)     │
│     │ Module │    │  Module  │    │ Module │                        │
│     └────────┘    └──────────┘    └────────┘                        │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

### Layer Breakdown

| Layer | Purpose | Technology |
|-------|---------|------------|
| **Frontend** | User interface | Next.js 14 (App Router), React 19, TypeScript, Tailwind CSS |
| **API** | REST endpoints, business logic | FastAPI, Uvicorn, Python 3.14+ |
| **Database** | Data persistence | SQLAlchemy ORM, SQLite (dev) / PostgreSQL (prod) |
| **Plugins** | Integration lifecycle | Custom framework with CONNECT→AUTH→FETCH→NORMALIZE→VALIDATE→STORE |

---

## Tech Stack

### Backend (API)

| Package | Version | Purpose |
|---------|---------|---------|
| `fastapi` | 0.110.0 | Web framework |
| `uvicorn[standard]` | 0.30.0 | ASGI server |
| `sqlalchemy` | 2.0.29 | ORM |
| `pydantic` | 2.7.1 | Data validation |
| `pydantic-settings` | 2.2.1 | Environment config |
| `python-jose[cryptography]` | 3.3.0 | JWT handling |
| `passlib[bcrypt]` | 1.7.4 | Password hashing |
| `python-dotenv` | 1.0.1 | Environment loading |

### Frontend (Web)

| Package | Version | Purpose |
|---------|---------|---------|
| `next` | 16.3.2 | React framework |
| `react` | 19.2.8 | UI library |
| `react-dom` | 19.2.8 | DOM bindings |
| `tailwindcss` | 4 | CSS framework |
| `@tailwindcss/postcss` | 4 | PostCSS integration |
| `typescript` | ^5 | Type safety |
| `eslint` | ^9 | Code linting |

---

## Repository Structure

```
personal-life-os/
├── apps/
│   ├── api/                          # FastAPI backend
│   │   ├── main.py                   # FastAPI app entry point
│   │   ├── db.py                     # Database configuration
│   │   ├── auth.py                   # Authentication utilities
│   │   ├── models.py                 # SQLAlchemy models
│   │   ├── requirements.txt          # Python dependencies
│   │   └── Dockerfile                # API container build
│   └── web/                          # Next.js frontend
│       ├── src/
│       │   ├── app/                  # Next.js App Router pages
│       │   │   ├── page.tsx          # Home page
│       │   │   ├── login/            # Auth pages (structure)
│       │   │   ├── dashboard/        # Main dashboard
│       │   │   ├── life/             # Life module page
│       │   │   ├── machine/          # Machine monitor page
│       │   │   ├── art/              # Art module page
│       │   │   └── time/             # Time ROI page
│       │   └── components/           # Reusable components
│       │       └── ui/
│       │           ├── button.tsx
│       │           └── card.tsx
│       ├── package.json              # NPM dependencies
│       └── tsconfig.json             # TypeScript config
│
├── packages/                         # Shared code
│   ├── schemas/                      # Pydantic/TypeScript schemas
│   │   ├── __init__.py
│   │   ├── base.py                   # SQLAlchemy Base
│   │   └── schemas.py                # API schemas
│   ├── config/                       # Configuration loading
│   └── utils/                        # Shared utilities
│
├── integrations/                     # Integration plugins
│   ├── github/                       # GitHub plugin
│   │   └── plugin.py
│   ├── workouts/                     # Workout tracking
│   ├── reading/                      # Reading tracking
│   ├── calendar/                     # Calendar integration
│   └── screen-time/                  # Screen time tracking
│
├── modules/                          # Feature modules
│   ├── life/                         # Life data aggregation
│   ├── machine-detective/            # System monitoring
│   ├── generative-art/               # Art generation
│   └── doomscroll-roi/               # Time ROI analysis
│
├── infrastructure/
│   ├── docker/                       # Docker configs
│   └── database/                     # DB migrations/seeds
│       └── init.sql                  # Initial schema
│
├── phases/                           # Development phases
│   ├── phase-01-v01-foundation/      # V0.1 foundation
│   ├── phase-02-life-data/           # Life module
│   ├── phase-03-machine/             # Machine module
│   ├── phase-04-art/                 # Art module
│   ├── phase-05-time-roi/            # Time ROI module
│   └── phase-06-ai/                  # AI analysis
│
├── docs/
├── .env.example                      # Environment template
├── docker-compose.yml                # Container orchestration
└── README.md
```

---

## Local Development Setup

### Prerequisites

- **Python 3.14+** - for the API backend
- **Node.js 20+** - for the web frontend
- **npm** or **yarn** - Node package manager
- **uv** (recommended) - Python package manager

### Step 1: Clone and Navigate

```bash
cd personal-life-os
```

### Step 2: Setup Environment Variables

Copy the example environment file:

```bash
cp .env.example .env
```

Edit `.env` with your values. For development, the defaults work:

```
API_URL=http://localhost:8000
API_VERSION=v1
DATABASE_URL=sqlite:///./personalife.db
JWT_SECRET_KEY=dev-secret-key-for-v0.1
```

### Step 3: Setup Python Backend

```bash
# Navigate to API directory
cd apps/api

# Create virtual environment (if not using uv)
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run database migrations (if any)
# For V0.1, tables are auto-created on startup
```

### Step 4: Setup Node Frontend

```bash
# Navigate to web directory
cd ../web  # or cd ../apps/web

# Install dependencies
npm install

# Run development server
npm run dev
```

### Step 5: Run API Server

```bash
# From the api directory
cd ../api  # or cd ../apps/api

# Run the FastAPI server
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

### Step 6: Access the Application

- **Web Interface**: http://localhost:3000
- **API Documentation**: http://localhost:8000/docs (Swagger UI)
- **API Health**: http://localhost:8000/health

---

## Docker Compose Setup

V0.1 includes Docker Compose configuration for containerized development.

### Prerequisites

- Docker Desktop or Docker Engine
- Docker Compose

### Step 1: Build and Start Containers

```bash
docker-compose up --build
```

### Step 2: Run Frontend Separately

The web app runs outside Docker in V0.1:

```bash
cd apps/web
npm run dev
```

### Container Services

| Service | Port | Description |
|---------|------|-------------|
| API | 8000 | FastAPI server |
| Web | 3000 | Next.js (run separately) |

Note: For V0.1, PostgreSQL is not configured - SQLite is used for development.

---

## Environment Variables

Create a `.env` file in `apps/api/` with:

```bash
# API Configuration
API_URL=http://localhost:8000
API_VERSION=v1

# Database Configuration
DATABASE_URL=sqlite:///./personalife.db  # SQLite for dev

# JWT Configuration
JWT_SECRET_KEY=your-super-secret-key-change-this-in-production
JWT_ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=60

# GitHub Integration (optional for development)
GITHUB_CLIENT_ID=
GITHUB_CLIENT_SECRET=
GITHUB_ACCESS_TOKEN=  # Personal token for testing

# Google Calendar Integration (optional)
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
```

---

## Database Setup

### SQLite (Development)

SQLite is the default for V0.1. No setup required - the database file is created automatically when the API starts.

```bash
# Database file location
apps/api/personalife.db
```

### PostgreSQL (Production)

To use PostgreSQL, update your `DATABASE_URL`:

```bash
# Environment variable format
DATABASE_URL=postgresql://user:password@localhost:5432/database_name

# Or with docker-compose
DATABASE_URL=postgresql://personalife:personalife@db:5432/personalife
```

The initial schema is defined in `infrastructure/database/init.sql`.

---

## API Endpoints Currently Implemented

### Public Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/` | Root welcome message | No |
| GET | `/health` | Health check | No |
| GET | `/api/v1/health` | API health check | No |

### Authentication Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/token` | Login (returns JWT token) | No |

### User Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/users/me` | Get current user info | Yes (mock) |

### Data Models (Schema)

The following models are defined (tables created on startup):

| Model | Purpose |
|-------|---------|
| `User` | User accounts with email, password, name |
| `GitHubCommit` | GitHub commit history |
| `WorkoutEntry` | Workout tracking |
| `ReadingEntry` | Book/reading tracking |
| `CalendarEvent` | Calendar events |
| `ScreenTimeEntry` | Screen time tracking |
| `MachineMetric` | System performance metrics |
| `DailyAggregate` | Precomputed daily summaries |

---

## Frontend Setup

The web application is built with Next.js 14 (App Router).

### Page Structure

| Route | Status | Description |
|-------|--------|-------------|
| `/` | ✅ Implemented | Home page with dashboard cards |
| `/login` | ⚠️ Placeholder | Authentication page (structure exists) |
| `/dashboard` | ⚠️ Placeholder | Dashboard page (UI ready, content to be filled) |
| `/life` | ⚠️ Placeholder | Life module page (UI ready) |
| `/machine` | ⚠️ Placeholder | Machine monitor page (UI ready) |
| `/art` | ⚠️ Placeholder | Art module page (UI ready) |
| `/time` | ⚠️ Placeholder | Time ROI page (UI ready) |

### UI Components

| Component | Location | Purpose |
|-----------|----------|---------|
| `Button` | `components/ui/button.tsx` | Styled button |
| `Card` | `components/ui/card.tsx` | Card container |

### Component Features

- **Dark Mode Support**: Built-in dark mode with Tailwind
- **Responsive Design**: Mobile-first with grid layouts
- **Link Navigation**: Next.js Link components for client-side routing

---

## How to Run the Complete System

### Development Mode (Recommended)

1. **Start the API**:
   ```bash
   cd apps/api
   uvicorn main:app --host 0.0.0.0 --port 8000 --reload
   ```

2. **Start the Web App** (new terminal):
   ```bash
   cd apps/web
   npm run dev
   ```

3. **Open in browser**: http://localhost:3000

### Docker Compose Mode

1. **Build and run containers**:
   ```bash
   docker-compose up --build
   ```

2. **Run web app separately**:
   ```bash
   cd apps/web
   npm run dev
   ```

Note: Docker Compose in V0.1 uses SQLite, not PostgreSQL.

---

## How to Verify V0.1 is Working

### Verification Checklist

| Test | Command/Action | Expected Result |
|------|----------------|-----------------|
| 1. Home page loads | Open http://localhost:3000 | Shows "Your Personal Data Platform" |
| 2. API responds | curl http://localhost:8000 | Returns `{"message":"Welcome..."}` |
| 3. Health check | curl http://localhost:8000/health | Returns `{"status":"healthy",...}` |
| 4. Swagger UI | Open http://localhost:8000/docs | Shows API documentation |
| 5. Tables created | Check `apps/api/personalife.db` | Database file exists with tables |

### Test API Endpoints

```bash
# Root endpoint
curl http://localhost:8000/

# Health check
curl http://localhost:8000/health

# Login (returns JWT token)
curl -X POST http://localhost:8000/token \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "username=testuser&password=testpass"

# Get user info (requires token)
curl http://localhost:8000/users/me \
  -H "Authorization: Bearer YOUR_TOKEN_HERE"
```

### Database Verification

```bash
# Check database tables
sqlite3 apps/api/personalife.db ".tables"

# Expected output:
# calendar_events  reading_entries   users
# daily_aggregates  screen_time_entries
# github_commits  workout_entries
# machine_metrics
```

---

## Authentication Status

### What's Implemented (V0.1)

| Feature | Status | Notes |
|---------|--------|-------|
| JWT Token Generation | ✅ | `auth.py` with `create_access_token()` |
| Password Hashing | ✅ | Using passlib with bcrypt |
| OAuth2 Scheme | ✅ | `OAuth2PasswordBearer` configured |
| Login Endpoint | ✅ | `/token` endpoint accepts credentials |
| User Model | ✅ | SQLAlchemy User model with hashed_password |
| Token Validation Logic | ✅ | `get_current_user()` function |

### What's NOT Implemented (V0.1)

| Feature | Status | Notes |
|---------|--------|-------|
| Real Credential Verification | ❌ | Accepts any credentials for demo |
| Protected Route Middleware | ❌ | No `@Depends(get_current_user)` on endpoints |
| Frontend Auth Flow | ❌ | Login page structure exists, no real implementation |
| Token Refresh | ❌ | No refresh token mechanism |
| Session Management | ❌ | No logout or session handling |
| OAuth2 Flow | ⚠️ | Partial - connect() works, authenticate() returns mock |

### Current State

Authentication is **partially implemented** for V0.1:

- The auth system is in place but accepts any credentials for development
- No endpoints currently require authentication (security by obscurity)
- The frontend has login page structure but no actual authentication flow
- Token-based authentication is ready for production once credential verification is enabled

---

## Current Project Status

### V0.1 - Foundation (Current)

**Status**: ✅ Complete

| Component | Status |
|-----------|--------|
| Project Structure | ✅ |
| API Backend | ✅ |
| Web Frontend | ✅ |
| Database Models | ✅ |
| Docker Compose | ✅ |
| Plugin Framework | ✅ |
| GitHub Integration | ✅ |
| UI Components | ✅ |

### Phases (Roadmap)

| Phase | Name | Status | Description |
|-------|------|--------|-------------|
| 01 | V0.1 Foundation | ✅ Done | Walking skeleton with basic app |
| 02 | Life Data | ⏳ Pending | Complete life module with all integrations |
| 03 | Machine | ⏳ Pending | System monitor with psutil |
| 04 | Art | ⏳ Pending | Generative artwork from life data |
| 05 | Time ROI | ⏳ Pending | Screen time → productivity analysis |
| 06 | AI | ⏳ Pending | Pattern finding and insights |

---

## Out of Scope for V0.1

This section explicitly defines what is NOT included in V0.1:

### Not Implemented

| Feature | Reason |
|---------|--------|
| Full OAuth2 flow with redirect URIs | Simplified for V0.1 demo |
| Frontend authentication flow | Structure exists, not wired |
| Real user credentials verification | Accepts any credentials for demo |
| PostgreSQL database | SQLite used for simplicity |
| Docker Compose PostgreSQL service | Not configured in V0.1 |
| Protected API routes | All routes are public |
| Module-specific endpoints | Life/Machine/Art/Time pages are placeholders |
| Background job scheduler | No automated sync tasks |
| Email notifications | Not implemented |
| Mobile app | Web-only for V0.1 |
| Real-time WebSocket support | Future enhancement |
| File upload functionality | Not in scope |

### Known Limitations

- Database: SQLite only (no PostgreSQL in V0.1 compose file)
- Authentication: Demo mode only (no real user validation)
- Modules: UI exists, functionality is placeholder
- Integrations: GitHub plugin exists but requires manual setup
- Background Jobs: No APScheduler integration yet

---

## Future Roadmap

These phases are planned but **NOT YET IMPLEMENTED**:

### Phase 02 - Life Data Module

- Complete `/api/v1/life/*` endpoints
- Integrate all integration plugins
- Build data aggregation service
- Create dashboard with real metrics
- Add CSV import for manual entries

### Phase 03 - Machine Module

- psutil-based system monitoring
- CPU/RAM/Disk/Network metrics collection
- Correlation engine for performance analysis
- Dashboard with historical charts

### Phase 04 - Art Module

- Deterministic generative artwork
- Daily artwork generation
- Gallery page with data visualization

### Phase 05 - Time ROI Module

- Screen time import (iOS/Android)
- Weekly ROI report generation
- Conversion engine (minutes → output units)

### Phase 06 - AI Module

- Pattern discovery
- Correlation analysis
- Predictive models
- Natural language interface

---

## Troubleshooting

### Common Issues and Solutions

#### Issue: API fails to start

**Error**: `ModuleNotFoundError: No module named 'schemas'`

**Solution**:
```bash
# Ensure you're in the correct directory
cd apps/api

# Verify Python can find the packages directory
export PYTHONPATH=$PYTHONPATH:$(pwd)/../..
python -c "import schemas; print('OK')"
```

#### Issue: Database file not created

**Error**: `sqlite3.OperationalError: no such table`

**Solution**:
```bash
# Database is auto-created on startup
# If table doesn't exist, restart the API
cd apps/api
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

#### Issue: Frontend can't connect to API

**Error**: `Failed to fetch` or CORS error

**Solution**:
```bash
# Ensure API is running on port 8000
curl http://localhost:8000/health

# Check CORS is configured in apps/api/main.py
# AllowOrigins includes http://localhost:3000
```

#### Issue: Docker container fails

**Error**: `Cannot connect to the Docker daemon`

**Solution**:
```bash
# Verify Docker is running
docker ps

# If using Docker Desktop, start the application
```

#### Issue: Port already in use

**Error**: `Address already in use`

**Solution**:
```bash
# Find and kill process using port 8000
lsof -i :8000  # Linux/Mac
netstat -ano | findstr :8000  # Windows

# Or change port in docker-compose.yml or uvicorn command
```

---

## Development Principles

### Code Style

| Aspect | Standard |
|--------|----------|
| Python | PEP 8, type hints with `mypy` |
| TypeScript | ES2020+, strict mode |
| React | Functional components, hooks |
| Git | Conventional commits |

### Development Workflow

1. **Branching**: Feature branches off `main`
2. **Commits**: `type(scope): message` format
3. **PRs**: Required review before merge
4. **Testing**: Tests required for new features

### Design Patterns

| Pattern | Usage |
|---------|-------|
| Repository Pattern | Data access layer |
| Dependency Injection | Database sessions, services |
| Middleware | CORS, authentication |
| Component Composition | UI components |

### Security Considerations

- **Current**: Development-only, no security hardening
- **Production**: JWT with secure secret, HTTPS, CORS restrictions
- **Password**: Bcrypt hashing, minimum 6 characters
- **Environment**: Secrets from environment variables, never committed

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Contributing

Contributions are welcome! Please follow these guidelines:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** your changes (`git commit -m 'feat: add amazing feature'`)
4. **Push** to the branch (`git push origin feature/amazing-feature`)
5. **Open** a Pull Request

---

## Acknowledgments

- FastAPI team for an excellent Python web framework
- Next.js team for the React framework
- All open source dependencies that make this possible

---

## Contact

For questions or feedback, please open an issue on GitHub.

---

**Built with Claude Code** 🤖
