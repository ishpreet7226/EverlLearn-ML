# 📦 EverLearn ML — Self-Improving MLOps Pipeline

An *end-to-end machine learning lifecycle pipeline* that uses GitOps principles, **FastAPI**, **MLflow**, and **GitHub Actions** to:

✔ Serve models via REST
✔ Track experiments and versions
✔ Automate retraining via scheduled or event-based processes
✔ Reload and promote models in production
✔ Enable feedback-driven improvements

This repo adapts and builds on the original model-retraining-gitops-fastapi design for production-oriented self-learning ML workflows. ([GitHub][1])

---

## 🚀 Project Overview

This system demonstrates a *practical, automated MLops pipeline* capable of:

* Continuous model evaluation and retraining
* Experiment logging and model registry with MLflow
* FastAPI inference service
* GitHub Actions-driven CI/CD retraining
* Automated production model promotion

This is **EverLearn ML**: offline training + feedback loop + automated retraining. ([GitHub][1])

---

## 🧠 System Flow

1. **Training:** Runs a model training script and logs runs + artifacts to MLflow.
2. **Model Registry:** MLflow stores model versions with aliases (e.g., `prod`, `staging`).
3. **Inference Service:** FastAPI serves predictions via REST.
4. **Trigger API:** FastAPI endpoint triggers retraining workflows.
5. **GitHub Actions:** Automates retrain → build → deploy steps based on schedules or external triggers.
6. **Auto Reload:** FastAPI reloads the latest `prod` model from MLflow. ([GitHub][1])

---

## 🧪 Key Technologies

| Component             | Purpose                                        |
| --------------------- | ---------------------------------------------- |
| **FastAPI**           | Production-grade REST inference service        |
| **MLflow**            | Experiment tracking & model registry           |
| **GitHub Actions**    | CI/CD & automated retraining workflows         |
| **Docker**            | Containerization for deployment                |
| **GitOps Principles** | Automated lifecycle control via GitHub updates |

*(Using best-practices inspired by Google’s MLOps automation recommendations.)* ([GitHub][2])

---

## 📁 Repository Structure

```
.
├── .github
│   └── workflows
│       ├── ci-cd.yml                # Continuous Integration & Docker workflow
│       └── retrain.yml              # Scheduled retraining workflow
├── app_model.py                     # FastAPI model serving & trigger endpoints
├── train.py                        # Model training & retraining logic
├── config.py                       # Config options for MLflow/registry
├── good.csv                       # Sample training dataset
├── requirements.txt               # Python dependencies
├── Dockerfile                    # Docker image specification
├── test_app.py                   # Inference service test suite
└── pyproject.toml                # Poetry config
```

---

## 📌 How It Works

### 1. **Training & Model Logging**

Training logic in `train.py`:

* Loads training data
* Trains a model
* Logs metrics & artifacts to MLflow
* Tags and registers a production-ready model

Models are registered and retrieved by alias (e.g., `@prod`) for serving. ([GitHub][1])

---

### 2. **FastAPI Service**

Endpoints include:

| Route           | Purpose                                         |
| --------------- | ----------------------------------------------- |
| `/predict`      | Returns model predictions                       |
| `/trigger`      | Triggers retraining workflow externally         |
| `/reload-model` | Reloads the latest production model from MLflow |

You can explore API docs at `/docs`. ([GitHub][1])

---

### 3. **CI/CD & Retraining Workflows**

Using GitHub Actions workflows in `.github/workflows`:

* `ci-cd.yml`: Tests, builds, and deploys the FastAPI service
* `retrain.yml`: Retrains the model on a schedule or via `/trigger`

You can enable scheduled retraining by uncommenting the cron schedule in `retrain.yml`. ([GitHub][1])

---

## 🛠️ Setup & Installation

### Install Requirements

```bash
pip install -r requirements.txt
```

OR use Poetry:

```bash
poetry install
```

### Configure Secrets

Add the following GitHub Actions secrets in your repository:

| Secret                | Purpose                                |
| --------------------- | -------------------------------------- |
| `MLFLOW_TRACKING_URI` | Endpoint to your MLflow server         |
| `REPO_TOKEN`          | GitHub token for triggering workflows  |
| `DATA_URL`            | (Optional) URL to external data source |
| `HOT_RELOAD_URL`      | Endpoint for FastAPI reload hook       |

Refer to `.github/workflows/retrain.yml` for retraining setup. ([GitHub][1])

---

## 📈 Deployment & Hosting

This pipeline can be deployed using:

* **Render / Railway / Cloud Run** – Hosting inference service
* **GCP / AWS / Azure** – Hosting MLflow tracking & registry
* **Docker Hub** – Container images

---

## 🧩 Extend for EverLearn Features

To turn this into a *self-improving ML system* like EverLearn:

✅ Add an API to collect **user feedback**
✅ Store feedback data in a database
✅ Expand `train.py` to load feedback as new training data
✅ Trigger GitHub Actions retraining when feedback count exceeds a threshold
✅ Add dashboards for model performance metrics

