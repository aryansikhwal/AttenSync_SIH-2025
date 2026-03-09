# AttenSync — RFID Attendance System (IoT + Full Stack + Analytics)

AttenSync is a **production-style attendance management system** that captures real-world RFID scans using **ESP32 + RFID-RC522**, sends them to a **Flask backend**, stores attendance in a database, and visualizes insights through a **React dashboard**.

This repository is designed to demonstrate **end-to-end system engineering**: hardware integration → backend APIs → database layer → frontend UI → analytics/prediction.

---

##  Project Summary     

-- Built a complete system end-to-end (hardware → cloud-style web app)  
-- API + database driven backend with real-time attendance ingestion  
-- Clean separation of concerns: **hardware service / backend service / UI**  
-- Works with both **live hardware input** and **simulated dummy scans** for testing/demo  
-- Deployable architecture with clear scope for scalability

---

## Team / Contributions

AttenSync was developed as a team project during SIH.

**My contributions:**
- Designed and implemented key backend APIs (Flask) for attendance operations
- Worked on database schema + integration (students, scans, attendance records)
- Contributed to analytics/prediction module and dashboard data endpoints


##  System Overview

### Problem
Manual attendance systems are slow, error-prone and not scalable.

### Solution
Use RFID cards/tags to automate attendance capture and provide:
- real-time attendance marking
- searchable student database
- attendance analytics
- forecasting (ML module)

---

##  System Architecture

```
┌─────────────────┐   RFID Scan   ┌───────────────────────────┐
│ ESP32 + RC522   │──────────────►│ Hardware Listener Service │
│ (RFID Reader)   │   BLE Serial  │ (Python)                  │
└─────────────────┘              └───────────────┬───────────┘
                                                 │ HTTP
                                                 ▼
                                      ┌──────────────────────┐
                                      │ Flask REST Backend    │
                                      │ - validation          │
                                      │ - auth/logging        │
                                      │ - attendance logic    │
                                      └──────────┬───────────┘
                                                 │ SQLAlchemy
                                                 ▼
                                      ┌──────────────────────┐
                                      │ Database (SQLite/PG) │
                                      │ - students           │
                                      │ - scans              │
                                      │ - attendance records │
                                      └──────────┬───────────┘
                                                 │ REST API
                                                 ▼
                                      ┌──────────────────────┐
                                      │ React Dashboard       │
                                      │ - student mgmt        │
                                      │ - live stats          │
                                      │ - attendance reports  │
                                      └──────────────────────┘
```

---

##  Key Engineering Features

### 1) Real RFID → Web Attendance Pipeline
- ESP32 scans a tag
- listener reads scan events over BLE/serial
- scan pushed to backend via REST API
- backend updates attendance tables
- dashboard reflects new data

### 2) Offline / Demo Mode Support
Hardware devices are hard to keep always online in a repo demo.
So this project supports:
-  live RFID data from ESP32
-  simulated scan data for development/demo/testing

-  This reflects real-world engineering practice where systems support mock inputs for stable testing.

### 3) Backend API + DB-Driven Logic
- attendance is not stored in frontend state
- everything persists in DB
- all operations happen via REST APIs

### 4) Analytics + Forecasting
Attendance is summarized into dashboards and reports, and includes an ML module to forecast attendance patterns.

---

##  Tech Stack

**Frontend**
- React 18
- TailwindCSS
- Axios

**Backend**
- Flask
- SQLAlchemy
- Flask-CORS

**Database**
- SQLite (development)
- PostgreSQL-ready (production)

**Hardware / IoT**
- ESP32
- RFID-RC522
- BLE / Serial data handling

---

##  Repository Structure

```bash
AttenSync/
├── src/
│   ├── backend/             # Flask REST API + DB logic
│   ├── frontend/            # React UI
│   └── hardware/            # ESP32 + RFID listener scripts
├── docs/                    # Setup + deployment docs
├── scripts/                 # setup/start scripts
├── assets/                  # sample files / docs
└── requirements.txt
```

---

##  API Endpoints (Core)

| Endpoint | Method | Description |
|---------|--------|-------------|
| `/api/health` | GET | System status |
| `/api/students` | GET/POST | Student management |
| `/api/attendance` | GET/POST | Attendance operations |
| `/api/rfid/scans` | GET | Scan logs |
| `/api/stats/dashboard` | GET | Analytics for dashboard |

---

##  Local Setup

### Backend
```bash
pip install -r requirements.txt
python backend.py
```

### Frontend
```bash
cd src/frontend
npm install
npm start
```

---

##  Testing Without Hardware (Recommended)

If ESP32/RFID is unavailable, you can still run the full system using:
- dummy scan generator / simulated scan input scripts
- sample attendance DB records

This ensures:
- the backend & UI are always demo-ready
- reproducible results for recruiters/interviewers


---

##  Future Improvements

- WebSocket live updates (instead of polling)
- Role-based access control (Admin/Teacher/Student)
- Containerization (Docker Compose)
- Cloud deployment (Render/Vercel + Postgres)

---

##  Author

**Aryan Sikhwal**  
GitHub: https://github.com/aryansikhwal  
LinkedIn: www.linkedin.com/in/aryansikhwal
