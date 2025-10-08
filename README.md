# Network Security ML Platform

Production-ready machine learning system for network security threat detection and phishing classification. Implements end-to-end MLOps pipeline with automated data processing, model training, and deployment infrastructure.

![Python](https://img.shields.io/badge/python-v3.10+-blue.svg)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=flat&logo=docker&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-%234ea94b.svg?style=flat&logo=mongodb&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=flat&logo=fastapi)
![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=flat&logo=amazon-aws&logoColor=white)

## Core Features

**ML Pipeline**: Automated data ingestion, validation with drift detection, feature engineering, model training with hyperparameter optimization, and batch prediction capabilities.

**Data Infrastructure**: MongoDB integration, S3 cloud storage, data versioning, and artifact management with comprehensive logging.

**API Service**: FastAPI REST endpoints, web interface, CORS support, and file upload functionality.

**DevOps**: Docker containerization, GitHub Actions CI/CD, AWS ECR/S3 integration, and production deployment automation.

## Architecture

```
Data Sources → Data Pipeline → ML Pipeline → API Service
     ↓             ↓              ↓           ↓
   MongoDB    Artifacts      Monitoring   Web Interface
```

**Stack**: Python 3.10+, FastAPI, MongoDB, Scikit-learn, MLflow, Docker, AWS (S3/ECR), GitHub Actions

## Setup & Deployment

```bash
git clone https://github.com/samay-rajput/networksecurity.git
cd networksecurity
pip install -r requirements.txt

# Configure environment variables
cp .env.example .env  # Add MongoDB URL, AWS credentials

# Run locally
python app.py

# Docker deployment
docker build -t networksecurity .
docker run -p 8000:8000 --env-file .env networksecurity
```

## Usage

**Training Pipeline**: `python -c "from networksecurity.pipeline.training_pipeline import TrainingPipeline; TrainingPipeline().run_pipeline()"`

**Data Upload**: `python push_data.py`

**API Prediction**: `curl -X POST "http://localhost:8000/predict" -F "file=@data.csv"`

## Production Deployment

**AWS ECR/EC2**: Automated deployment via GitHub Actions with Docker containerization.

**Configuration**: Set GitHub secrets for AWS credentials, ECR URI, and MongoDB connection strings.

**Monitoring**: Comprehensive logging with artifact versioning and drift detection.

## Technical Implementation

**Modular Architecture**: Component-based design with separate modules for data processing, ML operations, cloud integration, and API services.

**MLOps Pipeline**: Automated training pipeline with data validation, feature engineering, model training, and artifact management.

**Production Features**: Exception handling, comprehensive logging, data drift detection, and cloud storage integration.

---

*Production-ready ML system for network security threat detection with enterprise-grade infrastructure and automation.*