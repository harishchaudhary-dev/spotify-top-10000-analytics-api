# Spotify Top 10,000 Songs Analytics API

A production-oriented **Python and FastAPI analytics backend** built around the Spotify Top 10,000 Songs dataset. The project transforms exploratory data analysis and statistical workflows into a modular, documented, and testable REST API suitable for integration with web applications, dashboards, and data-driven services.

## 🚀 Project Overview

The original analysis performs data cleaning, exploratory analysis, descriptive statistics, trend analysis, correlation analysis, and statistical hypothesis testing on Spotify song data.

This project extends that analytical workflow into a **backend service architecture** using:

* **Python**
* **FastAPI**
* **Pandas**
* **NumPy**
* **SciPy**
* **Pydantic**
* **Pytest**
* **Docker**
* **REST API / OpenAPI**

The backend separates HTTP/API concerns from analytical business logic, making the application easier to maintain, test, extend, and deploy.

---

## 🏗️ Architecture

```text
                    ┌──────────────────────┐
                    │   Client Application  │
                    │ React / Streamlit /   │
                    │ Dashboard / API Client │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │       FastAPI        │
                    │    REST Endpoints    │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │     API Routes       │
                    │ Validation & HTTP     │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │  Analytics Service   │
                    │ Business Logic       │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │    Pandas / SciPy    │
                    │ Data & Statistics    │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Spotify CSV Dataset  │
                    └──────────────────────┘
```

---

## 🎯 Key Engineering Features

### Backend Engineering

* Modular FastAPI application structure
* RESTful API design
* Request parameter validation
* Pydantic response models
* Environment-based configuration
* Service-layer architecture
* Centralized analytical business logic
* HTTP error handling
* OpenAPI/Swagger documentation

### Data Engineering

* CSV ingestion
* Duplicate record handling
* Missing-value analysis
* Data-type inspection
* Numerical/categorical feature separation
* Date parsing
* Release-year feature extraction
* Analytical feature preparation

### Statistical Analytics

* Descriptive statistics
* Mean
* Median
* Mode
* Trimmed mean
* Pearson correlation
* Correlation analysis
* Shapiro-Wilk normality testing
* Popularity correlation
* Release-year trend analysis

### API Analytics

* Top artists
* Top songs
* Top albums
* Songs by release year
* Dataset summary
* Feature correlations
* Statistical analysis endpoints

### DevOps

* Docker
* Docker Compose
* Environment configuration
* `.gitignore`
* Automated testing
* Reproducible development environment

---

## 📁 Project Structure

```text
spotify-top-10000-analytics-api/
│
├── app/
│   ├── api/
│   │   ├── __init__.py
│   │   └── routes.py
│   │
│   ├── core/
│   │   ├── __init__.py
│   │   └── config.py
│   │
│   ├── schemas/
│   │   ├── __init__.py
│   │   └── analytics.py
│   │
│   ├── services/
│   │   ├── __init__.py
│   │   └── spotify_service.py
│   │
│   ├── __init__.py
│   └── main.py
│
├── data/
│   └── top_10000_1950-now.csv
│
├── tests/
│   └── test_api.py
│
├── .env.example
├── .gitignore
├── Dockerfile
├── docker-compose.yml
├── Makefile
├── requirements.txt
└── README.md
```

---

# 📊 Analytics Capabilities

## Dataset Summary

Returns:

* Number of rows
* Number of columns
* Numerical features
* Categorical features
* Missing values
* Duplicate records

### Endpoint

```http
GET /api/v1/dataset/summary
```

---

## Top Artists

Returns the most frequently occurring artists in the dataset.

```http
GET /api/v1/artists/top?limit=10
```

Example response:

```json
[
    {
        "name": "Artist Name",
        "count": 25
    }
]
```

---

## Top Songs

```http
GET /api/v1/songs/top?limit=10
```

---

## Top Albums

```http
GET /api/v1/albums/top?limit=10
```

---

## Release Trends

Analyzes the number of songs released per year.

```http
GET /api/v1/trends/releases
```

Example:

```json
[
    {
        "year": 2018,
        "songs": 425
    },
    {
        "year": 2019,
        "songs": 510
    }
]
```

---

# 📈 Statistical Analysis

## Correlation Analysis

Calculates the relationship between numerical audio features and Spotify `Popularity`.

```http
GET /api/v1/analytics/correlations?limit=10
```

---

## Pearson Correlation

Analyze the relationship between two numerical features.

```http
GET /api/v1/analytics/pearson?feature_a=Energy&feature_b=Danceability
```

Response:

```json
{
    "feature_a": "Energy",
    "feature_b": "Danceability",
    "statistic": 0.1234,
    "p_value": 0.001,
    "n": 9500
}
```

---

## Shapiro-Wilk Test

Tests whether a numerical feature follows an approximately normal distribution.

```http
GET /api/v1/analytics/shapiro?feature=Danceability
```

For API stability, very large datasets are sampled before performing the test.

---

# 📋 Descriptive Statistics

```http
GET /api/v1/analytics/statistics
```

The service provides statistical measurements including:

```text
count
mean
std
min
25%
50%
75%
max
median
mode
trimmed mean
```

---

# ⚙️ Technology Stack

| Category            | Technology        |
| ------------------- | ----------------- |
| Language            | Python            |
| Backend             | FastAPI           |
| Validation          | Pydantic          |
| Data Processing     | Pandas            |
| Numerical Computing | NumPy             |
| Statistics          | SciPy             |
| Testing             | Pytest            |
| API Documentation   | OpenAPI / Swagger |
| Containerization    | Docker            |
| Orchestration       | Docker Compose    |
| Version Control     | Git / GitHub      |

---

# 🔧 Installation

## 1. Clone Repository

```bash
git clone https://github.com/harishchaudhary-dev/spotify-top-10000-analytics-api.git
cd spotify-top-10000-analytics-api
```

## 2. Create Virtual Environment

### Windows

```bash
python -m venv .venv
.venv\Scripts\activate
```

### Linux / macOS

```bash
python3 -m venv .venv
source .venv/bin/activate
```

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

# 🔐 Environment Configuration

Create a `.env` file:

```env
DATA_PATH=data/top_10000_1950-now.csv
```

The `.env` file is excluded from Git through `.gitignore`.

---

# ▶️ Run Application

Start the development server:

```bash
uvicorn app.main:app --reload
```

Application:

```text
http://127.0.0.1:8000
```

---

# 📚 API Documentation

FastAPI automatically generates interactive API documentation.

### Swagger UI

```text
http://127.0.0.1:8000/docs
```

### ReDoc

```text
http://127.0.0.1:8000/redoc
```

### Health Check

```http
GET /api/v1/health
```

---

# 🐳 Docker Deployment

Build and start the service:

```bash
docker compose up --build
```

The API will be available at:

```text
http://localhost:8000
```

Stop the containers:

```bash
docker compose down
```

---

# 🧪 Testing

Run the automated test suite:

```bash
pytest -q
```

The tests validate the core API behavior including:

* Root endpoint
* Health endpoint
* HTTP responses
* API availability

The service architecture also allows the analytics layer to be expanded with dedicated unit and integration tests.

---

# 🔄 Notebook-to-Backend Transformation

The original Spotify analysis workflow includes:

```text
Data Loading
     ↓
Data Cleaning
     ↓
Duplicate Detection
     ↓
Missing Value Analysis
     ↓
Feature Inspection
     ↓
Descriptive Statistics
     ↓
Artist / Song / Album Analysis
     ↓
Release Year Analysis
     ↓
Correlation Analysis
     ↓
Statistical Testing
```

The backend converts reusable analytical operations into API-accessible services:

```text
Notebook Analysis
       ↓
Reusable Business Logic
       ↓
Service Layer
       ↓
FastAPI Routes
       ↓
REST API
       ↓
Frontend / Dashboard / Client
```

This separation allows the analytical logic to be reused by multiple client applications.

---

# 🧠 Senior Developer Design Decisions

## Separation of Concerns

API routes are responsible for HTTP communication, validation, and response handling.

Analytical operations are implemented inside:

```text
app/services/spotify_service.py
```

This prevents business logic from being tightly coupled to FastAPI route handlers.

## Configuration Management

Application configuration is isolated in:

```text
app/core/config.py
```

Environment variables can therefore be changed without modifying application code.

## Schema Validation

API responses use Pydantic models to provide:

* Explicit API contracts
* Type validation
* Consistent response structures
* Automatic OpenAPI documentation

## Parameter Validation

Endpoints validate query parameters such as:

```text
limit >= 1
limit <= 100
```

This prevents invalid requests from unnecessarily reaching the data-processing layer.

## Deployment Isolation

Docker provides a consistent runtime environment across:

```text
Development
Testing
CI/CD
Production
```

---

# 🔮 Future Enhancements

The architecture is designed to support additional production capabilities.

### Database Layer

Replace CSV-based storage with:

```text
PostgreSQL
```

for scalable querying and persistent analytics.

### Caching

Add:

```text
Redis
```

to cache expensive analytical queries.

### Authentication

Introduce:

```text
JWT / OAuth2
```

for protected API endpoints.

### Observability

Add:

```text
Structured Logging
Prometheus
Grafana
OpenTelemetry
```

for production monitoring.

### ML Extension

A machine-learning layer can be added for:

```text
Popularity Prediction
Song Recommendation
Artist Recommendation
Song Similarity
Clustering
Genre Classification
```

The current project does **not** claim ML inference because the supplied notebook is an EDA/statistical analysis workflow.

---

# ☁️ Production Deployment Architecture

A future production deployment could use:

```text
                    Internet
                       │
                       ▼
                 Load Balancer
                       │
                       ▼
                 FastAPI Service
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
      PostgreSQL     Redis       Object Storage
          │            │            │
          └────────────┼────────────┘
                       │
                       ▼
                Analytics Layer
```

Containerized deployment can be extended to:

```text
Docker → AWS ECS / EKS / Kubernetes
```

---

# 🔒 Git Security

The following files are intentionally excluded:

```text
.env
*.pyc
__pycache__/
.pytest_cache/
```

Large datasets can also be excluded from Git:

```text
data/*.csv
```

If the dataset is large, consider:

```text
Git LFS
AWS S3
Azure Blob Storage
Google Cloud Storage
```

instead of committing it directly to the repository.

---

# 📌 GitHub Setup

Initialize Git:

```bash
git init
```

Add files:

```bash
git add .
```

Commit:

```bash
git commit -m "feat: build Spotify analytics backend"
```

Set main branch:

```bash
git branch -M main
```

Connect repository:

```bash
git remote add origin https://github.com/<YOUR_USERNAME>/spotify-top-10000-analytics-api.git
```

Push:

```bash
git push -u origin main
```

---

# 💼 Resume Project Description

**Spotify Top 10,000 Songs Analytics API | Python, FastAPI, Pandas, SciPy, Docker**

Engineered a production-oriented **FastAPI analytics platform** for the Spotify Top 10,000 Songs dataset, implementing modular data-processing and statistical services for ranking, trend, correlation, and hypothesis-testing workflows with Pydantic validation, automated testing, RESTful API design, and Dockerized deployment.

---

# 👨‍💻 Senior Developer Skills Demonstrated

**Backend Engineering:** Python, FastAPI, REST APIs, Pydantic, API Architecture

**Data Engineering:** Pandas, NumPy, Data Cleaning, Feature Engineering, Data Validation

**Statistical Engineering:** SciPy, Correlation Analysis, Hypothesis Testing, Descriptive Statistics

**Software Engineering:** Modular Architecture, Separation of Concerns, Service Layer, Error Handling

**Testing:** Pytest, API Testing

**DevOps:** Docker, Docker Compose, Environment Configuration

**Version Control:** Git, GitHub, Branching, Commits, Repository Management

---

# 📊 Project Status

```text
Backend API        ✅ Completed
Data Processing    ✅ Completed
Statistical APIs   ✅ Completed
API Documentation  ✅ Completed
Testing            ✅ Implemented
Docker             ✅ Implemented
GitHub Ready       ✅ Ready
ML Model           ⏳ Future Enhancement
Database           ⏳ Future Enhancement
Authentication     ⏳ Future Enhancement
Monitoring         ⏳ Future Enhancement
```

---

# ⭐ Portfolio Value

This project demonstrates the transition from **notebook-based data analysis to structured backend engineering**.

It showcases the ability to:

```text
Analyze Data
     ↓
Design Business Logic
     ↓
Build Backend Services
     ↓
Expose REST APIs
     ↓
Validate API Contracts
     ↓
Write Tests
     ↓
Containerize Application
     ↓
Prepare for Production
```

This makes the project suitable for a **Senior Python Developer / Backend Developer / Data Engineer / ML Engineer portfolio** while remaining accurate to the capabilities of the original Spotify analysis.
