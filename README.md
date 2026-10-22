# 🧠 NeuronX AI — Study Operating System for JEE & NEET

NeuronX AI is an intelligent Study Operating System engineered for students preparing for **JEE Main**, **JEE Advanced**, and **NEET**. It provides personalized study planning, real-time focus tracking, adaptive testing, spaced repetition flashcards, interactive mind mapping, and handwritten notes scanning.

---

## 🚀 Core Features

- **AI Tutor & Problem Solver** — Real-time Server-Sent Events (SSE) streaming tutor powered by Gemini (`gemini-2.5-flash`) with conversation context, step-by-step problem derivations, high-yield practice generation, and formula analysis.
- **Adaptive Quiz Engine** — Topic-scoped quizzes with authentic JEE/NEET negative marking (+4 / -1 marks for MCQs, numerical tolerance grading), closed-loop mastery updates, and weak topic detection.
- **Focus & Fatigue Detection** — Real-time computer vision analysis using MediaPipe Face Mesh over authenticated WebSockets. Measures blink rates, yawns, look-away duration, and fatigue scores with server-authoritative session persistence.
- **OCR Handwritten Note Scanner** — EasyOCR + OpenCV image preprocessing pipeline. Safely validates image signatures and sizes, extracts handwritten text, and generates spaced repetition flashcards.
- **Interactive Mind Maps** — Concept graphs powered by React Flow with deterministic hierarchical layouts, formula nodes, and full saved-map inspection.
- **Spaced Repetition Flashcards** — Modified SM-2 algorithm tracking review intervals, repetition counts, and ease factors with dedicated due-today filtering.
- **AI Study Scheduler** — Google OR-Tools CP-SAT constraint optimization engine that allocates daily sessions based on syllabus weightage, student weakness, and available study hours with break time modeling.
- **Analytics & Readiness Insights** — Transparent, explainable readiness calculations and indicative percentile ranges based on verified student progress, without fabricated model claims.

---

## 🏗️ Architecture & Project Structure

```
neuronx-ai/
├── backend/                   # FastAPI Python Application
│   ├── app/
│   │   ├── main.py           # Application entrypoint & health checks
│   │   ├── config.py         # Pydantic v2 settings with environment validation
│   │   ├── database.py       # Async SQLAlchemy 2.0 engine & session
│   │   ├── seed_data.py      # Idempotent syllabus seeding (JEE Main, Advanced, NEET)
│   │   ├── models/           # SQLAlchemy ORM models matching Alembic migrations
│   │   ├── schemas/          # Pydantic validation schemas
│   │   ├── routers/          # API endpoints (auth, study, quiz, ai, focus, ocr, etc.)
│   │   └── services/         # Business logic (AI, CV focus, OCR, scheduler, analytics)
│   ├── alembic/              # Database migration versions
│   ├── Dockerfile            # Python 3.11-slim production container
│   ├── requirements.txt      # Locked Python dependencies including aiosqlite & asyncpg
│   └── .env.example
├── frontend/                 # Next.js 14 App Router
│   ├── app/                  # App routes ((auth), (dashboard), layout, landing)
│   ├── components/           # Reusable UI components & layouts
│   ├── hooks/                # Zustand client stores
│   ├── lib/                  # Axios API client, utils, SM-2 logic
│   ├── Dockerfile            # Node.js production container
│   └── package.json
├── docker-compose.yml        # Multi-container orchestration (FastAPI + Next.js + Postgres + Redis)
└── .env.example              # Consolidated environment configuration
```

---

## 🛠️ Tech Stack & Requirements

- **Backend:** FastAPI, Python 3.11, SQLAlchemy 2.0 (async), Alembic, Pydantic v2, PostgreSQL / SQLite (aiosqlite)
- **Frontend:** Next.js 14, React 18, TypeScript, Tailwind CSS, Framer Motion, React Flow, Axios
- **AI & Optimization:** Google GenAI SDK (`@google/genai`), Google OR-Tools CP-SAT, Scikit-learn
- **Computer Vision & OCR:** OpenCV, MediaPipe Face Mesh, EasyOCR, Pillow

---

## 🏁 Quick Start Guide

### Option 1: Docker Compose (Full Stack)

Ensure Docker and Docker Compose are installed and running:

```bash
# 1. Copy consolidated environment file
cp .env.example .env

# 2. Build and start services
docker compose up --build
```

Access the applications:
- **Frontend App:** [http://localhost:3000](http://localhost:3000)
- **Backend API Docs:** [http://localhost:8000/docs](http://localhost:8000/docs)
- **Health Check:** [http://localhost:8000/health](http://localhost:8000/health)

---

### Option 2: Local Development Setup

#### 1. Backend Setup

**Linux / macOS:**
```bash
cd backend
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# Run migrations
alembic upgrade head

# Start FastAPI server
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

**Windows (PowerShell):**
```powershell
cd backend
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install -r requirements.txt

# Run migrations
alembic upgrade head

# Start FastAPI server
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```

#### 2. Frontend Setup

```bash
# In project root or /frontend
npm install
npm run dev
```

---

## 🧪 Testing

### Frontend Unit & Utility Tests

Frontend tests run via `tsx`:

```bash
# Run unit tests from workspace root
npm test

# Or directly in frontend directory
cd frontend
npm test
```

### Backend Tests

```bash
cd backend
pytest
```

---

## 🔑 Environment Configuration

Create a `.env` file in the root directory (based on `.env.example`):

```env
# AI Studio & Core Configuration
GEMINI_API_KEY="YOUR_GEMINI_API_KEY"
GEMINI_MODEL="gemini-2.5-flash"
APP_URL="http://localhost:3000"

# Backend Configuration (FastAPI)
DATABASE_URL="postgresql+asyncpg://postgres:postgres@localhost:5432/neuronx"
REDIS_URL="redis://localhost:6379/0"
SECRET_KEY="replace-with-a-secure-random-32-byte-hex-string-for-production"
ALGORITHM="HS256"
ACCESS_TOKEN_EXPIRE_MINUTES="60"
REFRESH_TOKEN_EXPIRE_DAYS="7"
OPENAI_API_KEY=""

# Frontend Configuration (Next.js)
NEXT_PUBLIC_API_URL="http://localhost:8000"
NEXT_PUBLIC_WS_URL="ws://localhost:8000"
```

---

## 📄 License

MIT License. Designed and engineered for academic rigor and student mastery.
