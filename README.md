# Network Security ML Platform

Production-ready machine learning system for network security threat detection and phishing classification. Implements end-to-end MLOps pipeline with automated data processing, model training, and deployment infrastructure.

![Python](https://img.shields.io/badge/python-v3.10+-blue.svg)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=flat&logo=docker&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-%234ea94b.svg?style=flat&logo=mongodb&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=flat&logo=fastapi)
![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=flat&logo=amazon-aws&logoColor=white)

## What It Does

This platform **detects phishing websites and network security threats** using machine learning classification. It analyzes 30+ features including URL characteristics, SSL certificates, domain information, page rank, and traffic patterns to predict whether a website is legitimate or malicious.

**Input**: Network traffic data or website characteristics (CSV upload or API request)  
**Output**: Binary classification (-1: Phishing/Malicious, 1: Legitimate) with prediction confidence

## How It Works

1. **Data Ingestion**: Imports phishing detection datasets from MongoDB or CSV files containing 30+ security features
2. **Data Validation**: Performs schema validation, missing value checks, and data drift detection against baseline
3. **Feature Engineering**: Applies preprocessing, scaling, and transformation to optimize for classification models
4. **Model Training**: Trains ensemble models (Random Forest, Gradient Boosting, AdaBoost, etc.) with hyperparameter tuning tracked via MLflow
5. **Model Evaluation**: Selects best performing model based on precision, recall, and F1-score metrics
6. **Deployment**: Exposes trained model via REST API for real-time predictions on new network data
7. **Monitoring**: Logs all predictions, tracks model performance, and detects data drift for retraining triggers

## Core Features

**ML Pipeline**: Automated data ingestion, validation with drift detection, feature engineering, model training with hyperparameter optimization, and batch prediction capabilities.

**Classification Models**: Ensemble learning with Logistic Regression, KNN, Decision Trees, Random Forest, AdaBoost, and Gradient Boosting.

**Data Infrastructure**: MongoDB integration, S3 cloud storage, data versioning, and artifact management with comprehensive logging.

**API Service**: FastAPI REST endpoints with `/train` for model training and `/predict` for real-time phishing detection, web interface for result visualization.

**DevOps**: Docker containerization, GitHub Actions CI/CD, AWS ECR/S3 integration, and production deployment automation.

## Use Cases

- **Real-time Phishing Detection**: Classify websites as legitimate or phishing attempts in production environments
- **Batch Analysis**: Process large datasets of network traffic for security audits
- **Security Monitoring**: Continuous monitoring with drift detection to identify emerging threat patterns
- **Research & Development**: Experiment tracking with MLflow and model versioning for security research

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