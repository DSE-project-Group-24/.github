# DSE-project-Group-24

## Architecture diagram
```

+-----------------------------------------------------------+
|                       FRONTEND                            |
|          (Role-based dashboards: Nurse, Doctor,           |
|           Hospital Admin, Government)                     |
+-------------------------------+---------------------------+
                                |
                                ▼
+-----------------------------------------------------------+
|                      API GATEWAY                          |
|            (JWT validation & Role enforcement)            |
+-------------+-------------------+-------------------------+
              |                   |                          
      +-------+----+       +------+--------+          +------+ 
      | Core Backend|       | Frequent Models|          | Infrequent Models |
      | (Auth, DB)  |       | (Doctors only) |          | (Govt/Admin only) |
      +------------+       +---------------+          +-------------------+
              \                   |                          /
               \                  |                         /
                \                 |                        /
                 +---------------------------------------+
                                |
                                ▼
                  +----------------------------+
                  |    Supabase PostgreSQL     |
                  |    (Row-Level Security)    |
                  +----------------------------+

```


## 2) Backend Folder Structure (3 Separate FastAPI Backends)

### a) Core Backend (Auth + DB + Nurse logic)

```
core_backend/
│
├── app/
│   ├── main.py               # FastAPI app entrypoint
│   ├── config.py             # DB, JWT secrets, Supabase config
│   ├── database.py           # Supabase/Postgres connection setup
│   ├── models/               # Pydantic and ORM models
│   │   ├── user.py
│   │   ├── patient.py
│   │   └── accident.py
│   ├── routers/
│   │   ├── auth.py           # Login, register, token refresh
│   │   ├── nurse.py          # Nurse-specific endpoints
│   │   ├── patients.py       # CRUD patients (Nurse + Admin)
│   │   ├── admin.py          # Hospital admin user mgmt
│   ├── services/
│   │   ├── auth_service.py
│   │   ├── nurse_service.py
│   │   └── patient_service.py
│   ├── utils/
│   │   ├── security.py       # JWT helpers (validate tokens etc.)
│   │   ├── role_check.py     # Role verification dependencies
│   │   └── logging.py
│   └── __init__.py
│
└── requirements.txt
```

### b) Frequent Models Backend (Doctor-only prediction models)

```
frequent_models_backend/
│
├── app/
│   ├── main.py
│   ├── config.py
│   ├── routers/
│   │   └── doctor_predictions.py    # All doctor model endpoints
│   ├── services/
│   │   ├── stay_duration_model.py
│   │   ├── discharge_model.py
│   │   ├── transfer_model.py
│   │   └── risk_factor_model.py
│   ├── utils/
│   │   └── model_loader.py
│   ├── security.py                  # JWT validation helpers (role checks)
│   └── __init__.py
│
└── requirements.txt
```

### c) Infrequent Models Backend (Gov/Admin prediction & analytics)

```
infrequent_models_backend/
│
├── app/
│   ├── main.py
│   ├── config.py
│   ├── routers/
│   │   └── gov_analytics.py         # Government & admin analytics endpoints
│   ├── services/
│   │   ├── association_rules_model.py
│   │   ├── rare_analysis_model.py
│   │   └── severity_distribution.py
│   ├── utils/
│   │   └── model_loader.py
│   ├── security.py                  # JWT validation helpers (role checks)
│   └── __init__.py
│
└── requirements.txt
```

## 3) API Endpoint Map (Role-Based)

### a) Core Backend (Auth + Nurse + Admin)

| Method | Endpoint                  | Role(s) Allowed      | Description                               |
| ------ | ------------------------- | -------------------- | ----------------------------------------- |
| POST   | `/auth/register`          | Admin                | Create doctor/nurse accounts for hospital |
| POST   | `/auth/login`             | All                  | Login, returns JWT token                  |
| POST   | `/auth/refresh`           | All                  | Refresh JWT token                         |
| GET    | `/auth/me`                | All                  | Get current user profile                  |
| GET    | `/nurse/patients`         | Nurse                | List patients in nurse's hospital         |
| POST   | `/nurse/patients/pending` | Nurse                | Add minimal patient data                  |
| PATCH  | `/nurse/patients/{id}`    | Nurse                | Update patient details                    |
| GET    | `/patients/{id}`          | Nurse, Admin, Doctor | View patient details                      |
| GET    | `/admin/users`            | Admin                | List hospital users                       |
| POST   | `/admin/users`            | Admin                | Create user (doctor/nurse)                |
| PATCH  | `/admin/users/{id}`       | Admin                | Update user info                          |
| DELETE | `/admin/users/{id}`       | Admin                | Delete user                               |


### b) Frequent Models Backend (Doctors Only)

| Method | Endpoint                        | Role(s) Allowed | Description                    |
| ------ | ------------------------------- | --------------- | ------------------------------ |
| POST   | `/predict/stay-duration`        | Doctor          | Predict hospital stay duration |
| POST   | `/predict/discharge-outcome`    | Doctor          | Predict discharge outcome      |
| POST   | `/predict/transfer-requirement` | Doctor          | Predict transfer requirement   |
| POST   | `/predict/risk-factors`         | Doctor          | Predict severity risk factors  |


### c) Infrequent Models Backend (Gov/Admin)

| Method | Endpoint                         | Role(s) Allowed | Description                     |
| ------ | -------------------------------- | --------------- | ------------------------------- |
| GET    | `/analytics/accident-trends`     | Government      | Accident trend forecasts        |
| GET    | `/analytics/association-rules`   | Government      | Association rules extraction    |
| GET    | `/analytics/severity-factors`    | Government      | Severity risk contributors      |
| GET    | `/analytics/severity-estimation` | Government      | Severity ratio-based estimation |
