# 📝 Notes App

A full-stack Note Taking application built with **FastAPI**, **React**, and **PostgreSQL**.  
Designed to be deployed on **Kubernetes (K8s)** on AWS EC2 instances.

---

## 🏗️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React |
| Backend | FastAPI (Python) |
| Database | PostgreSQL |
| Containerization | Docker + Docker Compose |
| Orchestration | Kubernetes (K8s) |

---

## 📁 Project Structure

notes-app/
├── backend/
│   ├── main.py           # FastAPI app & API routes
│   ├── models.py         # SQLAlchemy DB models
│   ├── schemas.py        # Pydantic schemas
│   ├── database.py       # DB connection setup
│   ├── requirements.txt  # Python dependencies
│   └── Dockerfile
├── frontend/
│   ├── src/
│   │   └── App.js        # Main React component
│   └── Dockerfile
├── docker-compose.yml
├── .gitignore
└── README.md

## ⚙️ Prerequisites

Make sure you have the following installed:

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)
- [Node.js](https://nodejs.org/) (for local dev only)
- [Python 3.11+](https://www.python.org/) (for local dev only)

---

## 🚀 Running the App

### Option 1 — Docker Compose (Recommended)

**1. Clone the repository**
```bash
git clone <your-repo-url>
cd notes-app
```

**2. Build and start all containers**
```bash
docker compose up --build
```

**3. Access the app**

| Service | URL |
|---|---|
| Frontend (React) | http://localhost:3000 |
| Backend API | http://localhost:8000 |
| API Swagger Docs | http://localhost:8000/docs |

**4. Stop all containers**
```bash
docker compose down
```

**5. Stop and remove volumes (wipes DB data)**
```bash
docker compose down -v
```

---

### Option 2 — Run Locally (Without Docker)

**1. Start PostgreSQL using Docker**
```bash
docker run -d --name notes-postgres \
  -e POSTGRES_USER=admin \
  -e POSTGRES_PASSWORD=admin123 \
  -e POSTGRES_DB=notesdb \
  -p 5432:5432 postgres:15
```

**2. Setup and run Backend**
```bash
cd backend
python -m venv venv
venv\Scripts\activate        # Windows
# source venv/bin/activate   # Mac/Linux
pip install -r requirements.txt
uvicorn main:app --reload
```

**3. Setup and run Frontend**
```bash
cd frontend
npm install
npm start
```

---

## 🔌 API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/notes` | Get all notes |
| POST | `/notes` | Create a new note (with optional file) |
| DELETE | `/notes/{id}` | Delete a note by ID |

---

## 🌿 Branches

| Branch | Purpose |
|---|---|
| `main` | Local development version |
| `k8s-deployment` | Kubernetes manifests & deployment configs |

---

## ☸️ Kubernetes Deployment

> See the `k8s-deployment` branch for full K8s setup.

The app uses the following K8s objects:

| Object | Used For |
|---|---|
| Deployment | Frontend & Backend |
| StatefulSet | PostgreSQL |
| PersistentVolumeClaim (PVC) | PostgreSQL storage |
| ConfigMap | DB config (host, db name) |
| Secret | DB password |
| Service | Expose all components |

---

## 📦 Environment Variables

### Backend

| Variable | Default | Description |
|---|---|---|
| `DATABASE_URL` | `postgresql://admin:admin123@localhost:5432/notesdb` | PostgreSQL connection string |

---

## 👨‍💻 Author

Built for learning and practicing Kubernetes concepts on AWS EC2.