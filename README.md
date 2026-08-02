# Proctored Mock Test Platform

An enterprise-grade, full-stack MERN examination portal for competitive entrance tests (JEE, GATE, NEET) combining authentic exam player UI controls, optional client-side AI proctoring, deterministic grading analytics, and Google Gemini LLM-powered diagnostic reporting.

---

## Key Capabilities

1. **Adaptive Exam Engine**: Supports LaTeX math rendering via KaTeX, section timers, question palettes (Not Visited, Answered, Marked for Review), and single/multiple-choice/numerical inputs.
2. **Client-Side AI Proctoring (Optional)**: Real-time integrity evaluation using WebRTC webcam feeds, tab-switch detection, fullscreen enforcement, and face presence monitoring (missing face / multi-face alerts) with a zero server bandwidth footprint.
3. **Deterministic Grading & Dynamic Schema**: Calculates accuracy, speed per question, negative markings, and topic-wise performance deterministically without burning LLM API tokens.
4. **AI Strategic Diagnostics & Explainer**: Converts raw performance metrics into a personalized 3-week study plan, topic-by-topic breakdown, and step-by-step LaTeX solution explanations on demand using Google Gemini API (`gemini-2.5-flash`).

---

## Tech Stack

| Layer | Technology | Description |
| :--- | :--- | :--- |
| **Frontend** | React JS + Vite + Tailwind CSS | Fast SPA with responsive exam player, glassmorphism dark theme, and Lucide icons. |
| **Math & Viz** | KaTeX + Recharts | Client-side LaTeX formula rendering and interactive performance radar charts. |
| **Proctoring** | WebRTC + `@vladmandic/face-api` | Local browser face tracking, tab visibility listeners, and strike warning overlay. |
| **Backend API** | Node.js + Express.js | Asynchronous REST API server. |
| **Database** | MongoDB (Mongoose ORM) | Cloud database schema for `Users`, `Exams`, `Questions`, and `TestAttempts`. |
| **AI Integration**| Google Gemini API (`@google/genai`) | Structured JSON diagnostic generation and step-by-step STEM solution explanations. |

---

## Project Structure

```
proctoredmocktest/
├── README.md
├── frontend/                            (React JS Frontend)
│   ├── .env                             (VITE_API_BASE_URL)
│   ├── .gitignore
│   ├── package.json
│   ├── vite.config.js
│   └── src/
│       ├── assets/                      (Images, static media, global icons)
│       ├── components/                  (ExamPlayer, ProctoringHUD, MathRenderer, Analytics)
│       ├── context/                     (Exam & Proctoring state management)
│       ├── hooks/                       (Custom timers, webcam & face tracking hooks)
│       ├── pages/                       (Portal, ExamWindow, ResultsDashboard)
│       ├── services/                    (API calls to backend)
│       └── utils/                       (LaTeX parsing & score calculation helpers)
│
└── backend/                             (Node.js + Express + MongoDB Backend)
    ├── .env                             (PORT, MONGODB_URI, GEMINI_API_KEY)
    ├── .gitignore
    ├── package.json
    └── src/
        ├── config/                      (MongoDB connection via Mongoose)
        ├── controllers/                 (Exam, Attempt, AI Diagnostic controllers)
        ├── middleware/                  (Auth, error handling, validation)
        ├── models/                      (Mongoose Schemas: User, Exam, Question, Attempt)
        ├── routes/                      (API endpoints: /api/exams, /api/attempts, /api/ai)
        ├── services/                    (Deterministic scoring engine & Gemini LLM service)
        └── utils/                       (Seed datasets & scoring helpers)
```

---

## Getting Started

### Prerequisites
- **Node.js**: v18+ installed
- **MongoDB Atlas**: Connection URI string

### 1. Backend Setup

```bash
cd backend
npm install
```

Create a `.env` file in the `backend/` folder:
```env
PORT=5000
MONGODB_URI=your_mongodb_connection_string/proctoredmocktest_db
GEMINI_API_KEY=your_gemini_api_key_here
```

Start the backend server:
```bash
npm run dev
```
Health Check: `http://localhost:5000/api/health`

---

### 2. Frontend Setup

```bash
cd frontend
npm install
```

Create a `.env` file in the `frontend/` folder:
```env
VITE_API_BASE_URL=http://localhost:5000/api
```

Start the Vite development server:
```bash
npm run dev
```
Frontend App: `http://localhost:5173`

---

## License

MIT License
