# ByteForge — Enterprise Developer Cloud Platform

> Replit + GitHub + Vercel + VS Code — combined into one production-grade platform.

```
ByteForge/
├── frontend/     ← React 18 + Vite + Monaco Editor + Tailwind CSS
└── backend/      ← Node.js + Express + MongoDB + Redis + Socket.io + Docker
```

---

## 🚀 Quick Start

### 1. Backend

```bash
cd backend
npm install
cp .env.example .env      # fill in your secrets
npm run dev               # http://localhost:5000
```

**Required services:**
- MongoDB (local or Atlas)
- Redis (local or Upstash)
- Docker daemon (for code execution sandbox)

### 2. Frontend

```bash
cd frontend
npm install
cp .env.example .env.local
npm run dev               # http://localhost:3000
```

---

## 🏗 Frontend Architecture

```
src/
├── App.jsx                         # Routes (React Router v6)
├── main.jsx                        # Entry point
├── styles/globals.css              # Tailwind + custom CSS
├── components/
│   ├── auth/
│   │   └── AuthPage.jsx            # Login + Register + Google OAuth
│   ├── dashboard/
│   │   ├── Dashboard.jsx           # Home, stats, projects, charts
│   │   └── CreateProjectModal.jsx  # New project form
│   ├── ide/
│   │   ├── IDE.jsx                 # Main IDE layout (full)
│   │   ├── CodeEditor.jsx          # Monaco editor (custom theme)
│   │   ├── FileTree.jsx            # Explorer with context menu
│   │   ├── ConsolePanel.jsx        # Terminal + Output + Problems
│   │   ├── CollaborationPanel.jsx  # Live users + cursors + invite
│   │   ├── DeploymentPanel.jsx     # One-click deploy + history
│   │   ├── VersionPanel.jsx        # Version history + restore
│   │   └── SearchPanel.jsx         # Project-wide code search
│   └── shared/
│       ├── UI.jsx                  # Button, Badge, Input, Modal, Card...
│       ├── ProtectedRoute.jsx      # Auth guard
│       ├── ErrorBoundary.jsx       # React error boundary
│       ├── LoadingScreen.jsx       # Animated splash
│       └── NotFound.jsx            # 404 page
├── context/
│   ├── authStore.js                # Zustand — JWT auth + refresh
│   └── projectStore.js             # Zustand — files, tabs, content
├── services/
│   ├── api.js                      # Axios + auto token refresh interceptor
│   └── socket.js                   # Socket.io client service
└── utils/
    └── helpers.js                  # Language detection, formatters, etc.
```

### Key Tech — Frontend
| Library | Purpose |
|---|---|
| React 18 + Vite | UI framework + bundler |
| @monaco-editor/react | VS Code-grade editor |
| Tailwind CSS | Utility-first styling |
| Framer Motion | Animations |
| Zustand | Global state (auth, project) |
| Socket.io-client | Real-time collaboration |
| Recharts | Analytics charts |
| React Hot Toast | Notifications |
| React Router v6 | Client-side routing |
| Axios | HTTP client with interceptors |

---

## ⚙️ Backend Architecture

```
src/
├── server.js              # Express app entry
├── config/
│   ├── database.js        # MongoDB connection
│   ├── redis.js           # Redis/Bull setup
│   └── passport.js        # OAuth 2.0 (Google)
├── models/                # Mongoose schemas
│   ├── User.js
│   ├── Project.js
│   ├── File.js
│   └── Version.js
├── controllers/           # Request handlers
├── services/              # Business logic
│   ├── auth.service.js
│   ├── docker.service.js  # Sandboxed execution
│   ├── email.service.js
│   └── version.service.js
├── routes/                # API endpoints
├── middleware/            # Auth, rate limiting, validation
├── socket/                # Socket.io real-time events
├── jobs/                  # Bull background jobs
└── utils/                 # Logger, errors, helpers
```

### API Endpoints
```
POST   /api/v1/auth/register
POST   /api/v1/auth/login
POST   /api/v1/auth/refresh
GET    /api/v1/auth/google

GET    /api/v1/projects
POST   /api/v1/projects
DELETE /api/v1/projects/:id
POST   /api/v1/projects/:id/invite

GET    /api/v1/files/:projectId
POST   /api/v1/files
GET    /api/v1/files/:id/content
PATCH  /api/v1/files/:id
DELETE /api/v1/files/:id

POST   /api/v1/execute

GET    /api/v1/versions/:projectId
POST   /api/v1/versions
POST   /api/v1/versions/:id/restore

GET    /api/v1/deployments/:projectId
POST   /api/v1/deployments
```

---

## 🔐 Security Features

- JWT access tokens (15min) + refresh tokens (7d)
- RBAC (owner / collaborator / viewer roles)
- Google OAuth 2.0
- bcrypt password hashing (salt rounds: 12)
- Helmet.js security headers
- Rate limiting (100 req/15min)
- Joi input validation
- NoSQL injection prevention
- Docker sandboxed execution (CPU, RAM, PID limits)
- CORS strict config
- Environment variable secrets

---

## 🐳 Docker Compose

```bash
cd backend
docker-compose up --build
```

Starts: Express API + MongoDB + Redis + Nginx proxy

---

## 📦 Production Deployment

- **Frontend** → Vercel (`vercel deploy`)
- **Backend** → AWS / Render / Railway
- **Database** → MongoDB Atlas
- **Cache** → Upstash Redis
- **CI/CD** → GitHub Actions (`.github/workflows/ci-cd.yml`)

---

## 🌐 Environment Variables

See `frontend/.env.example` and `backend/.env.example` for all required variables.

## Author 

Vishal Maurya 
Virat Trivedi
