
# E-commerce-recommender-api (Collaborative Filtering)
<p align="center">
  <img src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white"/>
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white"/>
</p>

<p align="center">
  <b>High-Performance ML APIs · Collaborative Filtering · Production Ready</b>
</p>

## 🎯 Objective

Build a **Collaborative Filtering‑based Recommendation API** using FastAPI and PyTorch that:
- Ingests the Retailrocket E-commerce dataset from Kaggle
- Trains a collaborative recommendation model
- Serves recommendations via scalable API endpoints
- Uses Celery for asynchronous processing where needed

Dataset link: https://www.kaggle.com/datasets/retailrocket/ecommerce-dataset

---

## Phase 0 — Alignment & Setup

### Goals
- Understand the dataset structure and source files
- Define metrics and success criteria
- Establish environment standards

### Deliverables
- Project board with priorities
- Development & production environment defined
- Standard tech stack documentation

---

## Phase I — Data Acquisition & Understanding

### 1. Download RAW Dataset
```bash
kaggle datasets download -d retailrocket/ecommerce-dataset
```

### 2. Inspect Core Files
The dataset consists of:
- `events.csv`: user‑item interaction logs
- `item_properties.csv`: item attributes
- `category_tree.csv`: product category hierarchy

### 3. Define Key Features
- user_id
- item_id
- event_type (e.g., view, addtocart, transaction)
- timestamp

### Deliverables
- EDA report with interaction distributions
- Cleaned, filtered interaction dataset
- Defined schema for collaborative model

---

## Phase II — Data Preprocessing

### Steps
- Convert timestamps to datetime
- Filter interactions to relevant types (e.g., views/purchases)
- Create a user‑item interaction matrix for collaborative modeling
- Handle sparsity (e.g., minimum interactions threshold)

### Deliverables
- Preprocessing scripts in `services/ecommerce‑recommender/pipelines`
- Stored intermediate processed datasets
- Notebook documenting transformations

---

## Phase III — Model Training (Collaborative Filtering)

### Models to Evaluate
- **User‑based CF** — nearest neighbors
- **Item‑based CF**
- **Matrix Factorization / ALS / SVD**
- PyTorch embedding‑based CF

### Training Steps
1. Load processed interaction data
2. Build user–item matrix
3. Apply collaborative algorithm(s)
4. Evaluate with offline metrics (e.g., Precision@K, Recall@K)
5. Save best model artifacts

### Deliverables
- Model training scripts in `models/ecommerce/collaborative/`
- Trained model artifacts stored in `/artifacts/`
- Performance benchmark report

---

## Phase IV — API Development

### FastAPI Endpoints

| Endpoint | Purpose |
|----------|---------|
| `POST /api/v1/recs/predict` | Get top‑K recommendations |
| `GET /api/v1/recs/status/{id}` | Check task status |
| `POST /api/v1/recs/train` | Trigger async retrain |

### Steps
- Define Pydantic schemas
- Load trained model at startup
- Implement prediction logic in services

### Deliverables
- API routes under `services/ecommerce‑recommender/api/app/api/v1/`
- Health and docs endpoints

---

## Phase V — Async Processing (Celery + Redis)

### Tasks
- `train_model`: retrains collaborative model
- `backfill_recs`: compute top‑K scores offline
- Async status tracking

### Deliverables
- Celery config in `services/ecommerce‑recommender/celery_worker/`
- Redis broker + result backend
- Tasks with retry and logging

---

## Phase VI — Testing & Validation

### Test Types
- **Unit tests** for services & models
- **Integration tests** for API routes
- **E2E tests** for retrain + predict

### Deliverables
- `pytest` tests under `services/ecommerce‑recommender/api/tests/`
- Coverage reports
- Test data fixtures

---

## Phase VII — Containerization & Local Dev

### Docker
- Build images for backend & celery
- Shared network with Redis

### docker‑compose
Include services:
- `backend`
- `redis`
- `celery_worker`

### Deliverables
- Dockerfiles
- docker‑compose.yml

---

## Phase VIII — Logging & Monitoring

### Logging
- Structured JSON logs
- Correlation IDs

### Monitoring
- Prometheus metrics
- API latency & error dashboards

### Deliverables
- Logging config
- Dashboard templates

---

## Phase IX — Deployment

### Dev / Staging / Prod pipelines
- GitHub Actions workflows
- Feature flags for gradual rollout

### Deliverables
- infra scripts
- Deployment guides

---

## Phase X — Feedback & Iteration

### Goals
- Collect traffic logs
- Evaluate online metrics (CTR, conversion lift)
- Retrain periodically

### Deliverables
- Retraining schedule
- Automated pipelines

---

## Milestones & Timeline

| Milestone | Target Time |
|-----------|-------------|
| Data EDA & preprocessing | Week 1 |
| First collaborative model | Week 2 |
| API backend initial | Week 3 |
| Async workflows | Week 4 |
| Testing & Docker | Week 5 |
| Staging deployment | Week 6 |
| Production rollout | Week 7 |
| Iteration & Monitoring | Week 8+ |

---

## Notes

- Dataset interactions are implicit feedback (no explicit ratings); treat views/purchases accordingly.
- Start simple (e.g., ALS) then expand to neural CF in PyTorch.
- Prioritize observability and automated retraining.

---

## Tools & Libraries

✔ FastAPI  
✔ PyTorch  
✔ Celery + Redis  
✔ Docker + Compose  
✔ pytest  
✔ Prometheus/Grafana

---

## Next Steps

1. Agree on model versioning & artifact storage
2. Prepare raw dataset pipeline
3. Build preprocessing scripts
4. Start basic CF implementation

---
