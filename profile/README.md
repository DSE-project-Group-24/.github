# 🏥 Hospital Accident Analytics & ML‑Powered Decision Support System

🚀 A complete end‑to‑end accident data engineering and predictive healthcare platform built by **University of Moratuwa — DSE Group 24**.
This system digitalizes accident reporting and enhances medical decision‑making for hospitals while supporting national‑level health analytics.

---

## ✅ System Overview

We provide two core applications:

- 👨‍⚕️ **Frontend Web App** — Role‑based operations for hospitals and government authorities
- ⚙️ **FastAPI Backend + Supabase DB** — AI‑powered predictions & secure data access

---

## 🧩 System Architecture

```
DSE Accident Management & Analytics System
├── Frontend (React + Vite + Auth + ML UI)
└── Backend (FastAPI + Supabase + 6 ML Models)
    ├── Authentication (JWT)
    ├── Services (CRUD with role enforcement)
    ├── Accident Registry & Predictions
    └── Government Analytics APIs
```

---

## 🧑‍💼 Core User Roles & Functionalities

### 🏥 1️⃣ Hospital Admin

✅ Secure login via JWT

✅ Manage staff **within their hospital only**:- Add / update / remove **Doctors & Nurses**

✅ **No access** to other hospitals’ data
  
✅ **Cannot** view patient medical data

> 🔒 Strict access control ensures hospital‑scoped privacy

---

### 🩺 2️⃣ Doctor

✅ Access only to **their hospital’s** patients

✅ Search patient via name, NIC, or patient ID

✅ View **ongoing accidents only** with live ML predictions:

- ✅ **Estimated hospital stay duration**
 
- ✅ **Discharge outcome prediction**
 
- ✅ **Transfer requirement probability**

✅ Enter injury details to refine predictions
  
✅ View results as **charts + summaries**

> 🎯 Doctors get fast AI‑assisted decision support for patient triage

---

### 👩‍⚕️ 3️⃣ Nurse (Data Entry Personnel)

✅ Login restricted to their hospital

✅ Add new accident patients using minimal details (name, ward, BHD)

✅ Later complete full record (injuries, incident details)

✅ If injury severity missing → **Auto‑classification using ML**:

- Serious
- Mild / Moderate
- Unknown

✅ Cannot access or modify external hospital data

> 📝 Ensures fast reporting under emergency conditions

---

### 🏛️ 4️⃣ Government Authority

✅ Nationwide analytics dashboard

✅ Predictive insights for public safety planning:

- 📈 **Accident trend forecasts** (Time‑Series ML)

- 🔗 **Association Rules** (e.g., No helmet + Motorbike → Head Injury)

- ⚠️ **Severity risk factors** (top contributors to severe cases)

✅ **Unknown severity** records estimated using ratio‑based ML

> 📊 Supports data‑driven healthcare & policy decisions

---

## 🤖 Machine Learning Models Used

| Model                            | Purpose                             | Used By    |
| -------------------------------- | ----------------------------------- | ---------- |
| ✅ Severity Decision Tree Model  | Auto‑classifies severity if missing | Nurse      |
| ✅ Hospital Stay Duration Model  | Days patient stays                  | Doctor     |
| ✅ Discharge Outcome Model       | Recovery / transfer / death         | Doctor     |
| ✅ Transfer Requirement Model    | Transfer to larger hospital?        | Doctor     |
| ✅ Time‑Series Trend Forecasting | Future accident volume              | Government |
| ✅ Severity Risk Factor Model    | Contributor analysis                | Government |

> 🧠 All models integrated via API for real‑time inference

---

## 🔐 Authentication & Security

- JWT‑based role access
- Row‑level hospital restrictions
- Strong logging & audit tracking

---

## 📂 Repository Structure

```
DSE-project-Group-24
├── Frontend/        # React + Vite + ML Dashboards
└── Core-Backend/    # FastAPI + Supabase + 6 ML Models
```

---

## 🛠️ Tech Stack

- **Frontend:** React, Vite, Tailwind, Recharts
- **Backend:** FastAPI, Python, Supabase
- **ML:** Scikit‑Learn, Statsmodels, Pandas
- **Security:** JWT Auth

---

## 👥 Maintained By

**University of Moratuwa — DSE Group 24** 🇱🇰
