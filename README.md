```markdown
# Moodline – Mobile App for Early Burnout Detection

Moodline is a cross‑platform mobile app that helps users detect **early signs of burnout** by tracking mood, sleep, workload, and simple behavioral trends over time.[file:1][web:38]  
The app focuses on minimal friction, privacy, and clear, actionable insights instead of heavy manual self‑tracking.[file:1]

---

## Features

- **Daily mood check‑ins** with simple sliders/emojis for mood, stress, and energy plus optional short notes.[file:1]  
- **Sleep tracking** via quick manual input of sleep duration and quality (v1), with future potential for health API integration.[file:1]  
- **Workload tracking** using a simple workload level per day to approximate meeting and work intensity.[file:1]  
- **Burnout risk scoring** based on recent mood volatility, sleep disruption, and workload intensity, presented as low/medium/high risk with short explanations.[file:1][web:38]  
- **Trends dashboard** to visualize mood and sleep patterns over time and identify early warning signs.[file:1]  
- **Privacy controls** to toggle data streams and delete all personal data at any time.[file:1]  

> Moodline is a support tool and does **not** provide medical diagnosis or treatment.

---

## Tech Stack

- **Mobile frontend:** React Native + TypeScript  
- **Backend API:** FastAPI (Python)  
- **Database:** PostgreSQL  
- **State & data:** REST API with JWT‑based authentication  
- **Platform:** Android and iOS (React Native CLI)

This stack follows modern full‑stack patterns similar to existing FastAPI + TypeScript templates.[web:30][web:36]

---

## Project Structure

```
moodline/
├── frontend/                  # React Native app
│   └── src/
│       ├── assets/            # fonts, icons, images
│       ├── navigation/        # root, auth, main tab navigators
│       ├── screens/           # auth, home, checkin, trends, settings
│       ├── components/        # common UI, mood widgets, charts, settings
│       ├── store/             # auth + settings + app stores
│       ├── services/
│       │   └── api/           # API client and endpoints
│       ├── hooks/             # useAuth, useCheckin, useNotifications
│       ├── theme/             # colors, typography, spacing
│       ├── utils/             # date, validation, formatting
│       └── types/             # shared API/domain types
├── backend/                   # FastAPI backend
│   ├── app/
│   │   ├── main.py            # app entry and router mounting
│   │   ├── core/              # config, security, logging
│   │   ├── db/                # db session, migrations
│   │   ├── models/            # User, MoodEntry, SleepEntry, WorkloadEntry, RiskScore
│   │   ├── schemas/           # Pydantic schemas (auth, user, mood, sleep, workload, risk)
│   │   ├── api/
│   │   │   ├── deps.py        # dependencies (db, current_user)
│   │   │   └── routes/        # auth, users, mood, sleep, workload, risk
│   │   ├── services/          # risk engine, notifications, sentiment (local)
│   │   ├── tests/             # backend tests
│   │   └── utils/             # misc utilities
│   ├── pyproject.toml         # Python project metadata
│   ├── alembic.ini            # Alembic config
│   └── .env.example           # environment variable template
├── docs/                      # documentation
│   ├── product-spec.md        # detailed feature & UX description
│   ├── api-spec.md            # REST API endpoints and payloads
│   ├── architecture.md        # system architecture and data flows
│   └── privacy-ethics.md      # data handling and ethical considerations
├── .gitignore
└── README.md
```

This layout follows recommended React Native and FastAPI best practices, separating UI, domain logic, and infrastructure.[web:11][web:8][web:30]

---

## Getting Started

### Prerequisites

- Node.js and Yarn or npm  
- Python 3.11+  
- PostgreSQL instance (local or remote)  

Install the mobile dependencies (inside `frontend`):

```
cd frontend
yarn install     # or npm install
```

Install the backend dependencies (inside `backend`):

```
cd backend
python -m venv venv
# Windows:
venv\Scripts\activate
# macOS/Linux:
# source venv/bin/activate

pip install fastapi uvicorn[standard] sqlalchemy alembic psycopg2-binary python-jose[bcrypt] python-dotenv
```

---

### Running the Backend

1. Create a `.env` file from `.env.example` and fill in:
   - `DATABASE_URL` (PostgreSQL)
   - `SECRET_KEY`
   - `ACCESS_TOKEN_EXPIRE_MINUTES`
2. Run migrations with Alembic (once your migrations are defined).  
3. Start the API:

```
cd backend
uvicorn app.main:app --reload
```

FastAPI will expose automatic docs at `/docs` and `/redoc`.[web:36]

---

### Running the Mobile App

From the `frontend` folder:

```
cd frontend
# Start Metro bundler
yarn start

# In another terminal:
yarn android     # for Android
# or
yarn ios         # for iOS (macOS + Xcode required)
```

Update the API base URL in `src/services/api/client.ts` to point to your running backend.

---

## Core Concepts

- Moodline aggregates **mood, sleep, and workload** into interpretable trends to highlight early burnout risk instead of waiting until symptoms are severe.[file:1][web:38]  
- The system prioritizes **minimal user effort** by using short daily inputs and simple screens.[file:1]  
- All sensitive data is stored securely and can be fully deleted by the user from the app settings at any time.[file:1]

---

## Roadmap (v1 → Future)

- v1:
  - Manual mood, sleep, workload inputs
  - Simple rule‑based risk scoring and notifications
  - Privacy controls and account/data deletion  
- Future:
  - Optional integration with device health APIs for passive sleep tracking
  - Calendar‑based workload analysis
  - More advanced, interpretable ML models for risk scoring (while keeping transparency).[file:1][web:38]
