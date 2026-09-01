# Personal Life OS

A web-first personal data platform with a FastAPI backend and Next.js frontend.

## Overview

Personal Life OS is a monorepo project providing the foundation for a personal data dashboard. This is a **work in progress** - V0.1 represents the minimal viable platform structure.

### What's Implemented (V0.1)

- **FastAPI Backend**: Basic REST API with health checks and authentication utilities
- **Next.js Frontend**: Minimal web application with routing and placeholder pages
- **PostgreSQL**: Database setup with SQLAlchemy ORM
- **Docker Compose**: Container orchestration for local development
- **Authentication**: JWT token utilities and user model (foundation only)

### What's Not Implemented

- No working frontend pages (all show placeholders)
- No integration with external services (GitHub, calendar, etc.)
- No complete authentication flow
- No PostgreSQL connection in Docker (uses SQLite for development)
- No background job scheduling
- No production-ready security

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                           Personal Life OS                           │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  ┌──────────────┐         ┌──────────────┐         ┌──────────────┐ │
│  │   Web App    │ ←─────> │   FastAPI    │ ←─────> │  PostgreSQL  │ │
│  │  (Next.js)   │   API   │  (Python)    │  Data   │              │ │
│  │              │  Routes │              │  Flow   │              │ │
│  └──────────────┘         └──────────────┘         └──────────────┘ │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Tech Stack

### Backend

- **FastAPI** (0.110.0) - Web framework
- **Uvicorn** (0.30.0) - ASGI server
- **SQLAlchemy** (2.0.29) - ORM
- **Pydantic** (2.7.1) - Data validation
- **JWT** (python-jose) - Token authentication
- **Passlib** - Password hashing

### Frontend

- **Next.js** (14.3.2) - React framework
- **React** (19.2.8) - UI library
- **TypeScript** - Type safety
- **Tailwind CSS** - Styling

---

## Project Structure

```
personal-life-os/
├── apps/
│   ├── api/                    # FastAPI backend
│   │   ├── main.py            # API entry point
│   │   ├── db.py              # Database config
│   │   ├── auth.py            # Auth utilities
│   │   ├── models.py          # SQLAlchemy models
│   │   └── Dockerfile
│   └── web/                    # Next.js frontend
│       └── src/
│           └── app/           # Application pages
├── packages/                   # Shared code
│   ├── schemas/               # Pydantic models
│   ├── config/                # Configuration
│   └── utils/                 # Utilities
├── integrations/              # External service plugins
├── modules/                   # Feature modules
├── infrastructure/
│   └── database/              # DB migrations
├── .env.example
└── docker-compose.yml
```

---

## Setup

### Prerequisites

- Docker and Docker Compose
- Node.js 20+
- Python 3.14+

### Environment Variables

Copy `.env.example` to `.env` and update values:

```bash
cp apps/api/.env.example apps/api/.env
```

### Docker Compose

```bash
cd personal-life-os
docker-compose up -d
```

### Local Development

**Backend:**
```bash
cd apps/api
pip install -r requirements.txt
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

**Frontend:**
```bash
cd apps/web
npm install
npm run dev
```

---

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/` | Root endpoint |
| GET | `/health` | Health check |
| GET | `/api/v1/health` | API health check |
| POST | `/token` | Login (development only) |
| GET | `/users/me` | Get current user |

---

## Database

The application uses SQLAlchemy with PostgreSQL. The database schema is defined in `infrastructure/database/init.sql`.

---

## Future Roadmap

The following modules are planned but **NOT IMPLEMENTED** in V0.1:

- GitHub integration
- Workout tracking
- Reading tracking
- Calendar integration
- Machine monitor
- Generative art
- Time ROI analysis
- AI insights

See `PERSONAL_SYSTEMS_ROADMAP.md` for the complete roadmap.

---

## Development Status

**V0.1 - Foundation** (Current)

Status: ⚠️ Early development - API and frontend structure in place, but no functional features implemented yet.
