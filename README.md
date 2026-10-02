# AI-CyberShield

**Explainable Multilingual AI-Based Early Warning System for Digital-Fraud Detection**

> **Research Prototype** — Not validated for production use. Results are probabilistic.

---

## What It Does

AI-CyberShield analyses text messages (SMS, email, WhatsApp, social media) for digital fraud
indicators in three language contexts: **English**, **Marathi**, and **Hinglish**.

It returns:
- A fraud score (0–100%)
- A risk tier (LOW / MEDIUM / HIGH / CRITICAL)
- A list of fired rule-based patterns with matched excerpts
- ML model feature attribution (when model is trained)
- A plain-language explanation

---

## Repository Structure

```
AI-CyberShield/
├── backend/        # FastAPI app — all API and detection pipeline code
├── frontend/       # React + TypeScript web interface
├── ml/             # Offline model training (NEVER imported by backend at runtime)
├── docker-compose.yml
└── .env.example
```

---

## Quick Start

### Prerequisites
- Docker + Docker Compose, **or** Python 3.11 + Node 20 + PostgreSQL

### With Docker

```bash
cp .env.example .env
# Edit .env — set a real SECRET_KEY and database credentials
docker-compose up --build
```

- Frontend: http://localhost:5173
- Backend API: http://localhost:8000/docs

### Without Docker

**Backend:**
```bash
cd backend
pip install -e ".[dev]"
# Set DATABASE_URL in your environment or .env file
uvicorn app.main:app --reload
```



## ML Model Training

The ML model is trained **offline** and is **not required** for the application to run.
Without the model, rule-based detection still functions fully.

```bash
# 1. Place your dataset CSVs in ml/data/processed/
#    Format: text,label (0=legit, 1=fraud)
#    See ml/README.md for provenance guidance.

cd ml
pip install -e .
python src/train.py --config configs/experiment_v1.yaml

# Artifacts are saved to ml/artifacts/model_v1/
# Restart the backend to load the new model.
```

---

## Running Tests

```bash
cd backend
pytest tests/ -v
```

---

## Engineering Principles

- **No fabricated ML metrics** — metrics are only populated after real training
- **No fabricated datasets** — dataset provenance documented in `ml/README.md`
- **No hardcoded secrets** — all sensitive values in environment variables
- **Strict layer separation** — training ↔ inference ↔ API ↔ frontend are independent
- **Explainability first** — every result includes rule rationale and feature attribution
- **Honest prototype framing** — disclaimer displayed on every analysis result

---

## Tech Stack

| Layer     | Technology |
|-----------|------------|
| Frontend  | React 18, TypeScript, Vite |
| Backend   | Python 3.11, FastAPI, SQLAlchemy (async) |
| Database  | PostgreSQL 15 |
| ML/NLP    | scikit-learn, langdetect, LIME |
| Container | Docker, docker-compose |

---

## License

Research prototype. See individual dataset licenses in `ml/README.md`.
# 🛡️ AI-CyberShield

### AI-Powered Cyber Fraud Detection & Security Analysis Platform

AI-CyberShield is an intelligent cybersecurity platform designed to analyze potentially malicious digital activities, identify fraud indicators, and provide users with understandable security insights.

The system combines **Artificial Intelligence, cybersecurity analysis, risk assessment, and security monitoring** to help detect suspicious URLs, messages, activities, and other potential cyber threats.

---

## 🚀 Overview

Cyber fraud is becoming increasingly sophisticated. Phishing links, fake websites, malicious messages, impersonation, and social-engineering attacks can appear legitimate and may be difficult for ordinary users to identify.

**AI-CyberShield** aims to provide a centralized platform where suspicious digital content can be analyzed and converted into a simple security assessment.

The system analyzes available indicators, detects suspicious patterns, calculates a risk level, and presents the result through a professional security dashboard.

### Core Concept

```text
User Input
    ↓
Data Collection
    ↓
Preprocessing
    ↓
Feature / Indicator Extraction
    ↓
AI + Security Analysis
    ↓
Threat Detection
    ↓
Risk Assessment
    ↓
Security Report
    ↓
Recommended Action
```

---

# 🎯 Objectives

* Detect potentially fraudulent or malicious digital content.
* Identify common phishing and cyber-fraud indicators.
* Use AI-assisted analysis for security assessment.
* Provide understandable explanations instead of only showing technical results.
* Assign an appropriate risk level based on detected indicators.
* Maintain analysis history for future reference.
* Provide users with recommended security actions.
* Create a centralized cybersecurity monitoring interface.
* Help users understand *why* something may be suspicious.

---

# ✨ Key Features

## 🔍 1. AI Threat Analysis

The system analyzes submitted information and identifies suspicious characteristics using AI-assisted security analysis.

Possible analysis areas include:

* Suspicious URLs
* Phishing indicators
* Domain characteristics
* Message/content patterns
* Social-engineering indicators
* Suspicious keywords
* Redirect behavior
* Domain anomalies
* Potential impersonation
* Other security indicators

---

## 🧠 2. Risk Assessment

After analysis, the system generates a security risk assessment.

Example:

```text
Risk Level: HIGH

Threat Score: 87/100

Detected Indicators:
✓ Suspicious domain pattern
✓ Urgency-based language
✓ Credential harvesting indicators
✓ Unknown URL structure

Recommendation:
Do not enter personal or financial information.
```

The risk score is intended as an **assessment aid**, not as a guarantee that a website or message is malicious.

---

## 📊 3. Security Dashboard

The dashboard provides a centralized view of the system.

It can display:

* Total analyses
* Safe results
* Suspicious results
* High-risk detections
* Recent analyses
* Threat trends
* System status
* Detection statistics

Example:

```text
-----------------------------------------
        AI-CYBERSHIELD DASHBOARD
-----------------------------------------

Total Scans             1,248
Safe                     812
Suspicious               291
High Risk                145

Threat Detection Rate    94.2%

Recent Activity
-----------------------------------------
URL Analysis        HIGH       2 min ago
Message Analysis    LOW        8 min ago
URL Analysis        SAFE       15 min ago
-----------------------------------------
```

---

# 🕵️ 4. Analysis History

Every completed analysis can be stored in the system.

Users can review:

* Previous scans
* Analysis date and time
* Input type
* Risk level
* Threat score
* Detected indicators
* Security recommendations

This allows users to track previous security investigations.

---

# 📄 5. Detailed Security Reports

AI-CyberShield can generate detailed analysis reports containing:

### Input Information

What was analyzed.

### Detection Results

What suspicious indicators were found.

### Risk Assessment

Overall security risk.

### Explanation

Why the system considered the input suspicious.

### Recommended Action

What the user should do next.

Example:

```text
Security Analysis Report
────────────────────────────

Input Type: URL

Risk Level: HIGH
Threat Score: 91/100

Detected Indicators:
• Suspicious domain
• Possible phishing structure
• Credential collection pattern
• URL obfuscation

Recommended Action:
Avoid opening the URL and do not
provide credentials or financial information.
```

---

# 📡 6. System Status

The System Status section provides information about the health of the cybersecurity platform.

Possible components:

```text
AI Analysis Engine       ● Operational
Threat Detection         ● Operational
Database                 ● Operational
API Services             ● Operational
Authentication           ● Operational
Monitoring               ● Operational
```

It can also display:

* API availability
* Database connectivity
* AI engine status
* Last system check
* Analysis service status
* System uptime

---

# 🔐 7. Secure Authentication

The platform can provide secure authentication functionality including:

* User registration
* User login
* Session management
* Logout
* Protected pages
* Role-based access where required

Sensitive credentials should never be stored as plain text.

---

# 🤖 AI Analysis Architecture

The overall architecture can be represented as:

```text
                    ┌───────────────────┐
                    │      User         │
                    └─────────┬─────────┘
                              │
                              ▼
                    ┌───────────────────┐
                    │   Web Interface   │
                    └─────────┬─────────┘
                              │
                              ▼
                    ┌───────────────────┐
                    │   Backend / API   │
                    └─────────┬─────────┘
                              │
                 ┌────────────┴────────────┐
                 ▼                         ▼
        ┌─────────────────┐      ┌─────────────────┐
        │ Data Processing │      │ Security Checks │
        └────────┬────────┘      └────────┬────────┘
                 │                        │
                 └───────────┬────────────┘
                             ▼
                    ┌───────────────────┐
                    │   AI Analysis     │
                    │      Engine       │
                    └─────────┬─────────┘
                              │
                              ▼
                    ┌───────────────────┐
                    │ Risk Assessment   │
                    └─────────┬─────────┘
                              │
                              ▼
                    ┌───────────────────┐
                    │ Security Report   │
                    └─────────┬─────────┘
                              │
                              ▼
                    ┌───────────────────┐
                    │ User Dashboard    │
                    └───────────────────┘
```

---

# 🧩 Threat Detection Process

```text
1. User submits suspicious content
              ↓
2. System validates the input
              ↓
3. Input is normalized
              ↓
4. Security indicators are extracted
              ↓
5. AI analyzes the available information
              ↓
6. Threat indicators are evaluated
              ↓
7. Risk score is generated
              ↓
8. Threat category is determined
              ↓
9. Explanation is generated
              ↓
10. Security recommendation is displayed
              ↓
11. Result is stored in analysis history
```

---

# 🏗️ Project Structure

A possible project structure:

```text
AI-CyberShield/
│
├── frontend/
│   ├── components/
│   ├── pages/
│   ├── assets/
│   ├── services/
│   └── styles/
│
├── backend/
│   ├── controllers/
│   ├── routes/
│   ├── services/
│   ├── middleware/
│   ├── models/
│   └── utils/
│
├── ai-engine/
│   ├── models/
│   ├── preprocessing/
│   ├── feature-extraction/
│   └── analysis/
│
├── database/
│   ├── schema/
│   └── migrations/
│
├── docs/
│   ├── architecture/
│   └── reports/
│
├── .env.example
├── .gitignore
├── package.json
└── README.md
```

> The exact structure may differ depending on the technology stack used in the implementation.

---

# 🛠️ Technology Stack

The platform can be implemented using technologies such as:

| Layer           | Technology                                |
| --------------- | ----------------------------------------- |
| Frontend        | React / HTML / CSS / JavaScript           |
| Backend         | Node.js / Express                         |
| AI Layer        | Python / AI APIs / ML models              |
| Database        | PostgreSQL / MongoDB                      |
| API Testing     | Postman                                   |
| Version Control | Git / GitHub                              |
| Deployment      | Docker / Cloud Platform                   |
| Security        | HTTPS / Authentication / Input Validation |

---

# 🔌 API Architecture

The backend can expose REST APIs such as:

```text
POST   /api/auth/register
POST   /api/auth/login
POST   /api/analyze
GET    /api/analysis/history
GET    /api/analysis/:id
GET    /api/dashboard/statistics
GET    /api/system/status
POST   /api/report
POST   /api/auth/logout
```

### Example Analysis Request

```json
{
  "type": "url",
  "input": "https://example.com"
}
```

### Example Response

```json
{
  "riskLevel": "HIGH",
  "score": 87,
  "category": "Phishing",
  "indicators": [
    "Suspicious domain pattern",
    "Potential credential harvesting"
  ],
  "recommendation": "Avoid entering sensitive information."
}
```

---

# 🗄️ Data Management

The system can maintain records such as:

### Users

```text
user_id
name
email
password_hash
role
created_at
```

### Analysis

```text
analysis_id
user_id
input_type
input_data
risk_level
risk_score
threat_category
created_at
```

### Detection Indicators

```text
indicator_id
analysis_id
indicator_name
severity
description
```

### Reports

```text
report_id
analysis_id
report_type
generated_at
```

---

# 🔒 Security Considerations

AI-CyberShield itself should follow secure-development practices.

Important measures include:

* Password hashing
* HTTPS
* Authentication and authorization
* Input validation
* API authentication
* Rate limiting
* Secure session handling
* Environment variables for secrets
* Database access controls
* Protection against SQL injection
* Protection against XSS
* Protection against CSRF where applicable
* Secure error handling
* Logging and monitoring
* Avoiding sensitive information in logs

---

# ⚠️ Responsible Use

AI-CyberShield is designed for **defensive cybersecurity analysis and awareness**.

The system should be used to:

* Analyze potentially suspicious content
* Improve cybersecurity awareness
* Support security investigations
* Identify possible fraud indicators
* Educate users about cyber threats

The system should **not** be treated as an absolute authority. A low-risk result does not guarantee that content is safe, and a high-risk result does not by itself prove malicious intent.

Users should verify important security decisions through trusted sources and established security procedures.

---

# 📈 Future Enhancements

Possible future improvements include:

### Advanced AI Detection

* Machine-learning-based classification
* NLP-based phishing detection
* Behavioral analysis
* Anomaly detection
* Explainable AI

### Threat Intelligence

* Domain reputation checking
* IP reputation
* Malware intelligence
* Phishing databases
* Threat intelligence feeds

### Real-Time Monitoring

* Continuous URL monitoring
* Security alerts
* Real-time notifications
* Automated threat monitoring

### Advanced Reporting

* PDF security reports
* Investigation timelines
* Threat visualization
* Exportable reports

### Enterprise Features

* Admin dashboard
* Role-based access control
* Organization management
* Security team workflows
* Audit logs
* SIEM integration

---

# 📊 Example Risk Classification

| Risk Level | Example Interpretation |
| ---------- | ---------------------- |
| 🟢 Low     | Few or no suspici      |
#   A I - C i b e r S h i e l d  
 