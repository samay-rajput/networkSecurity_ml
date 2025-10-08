# 🛡️ Network Security ML Platform

A comprehensive machine learning platform for network security threat detection with a focus on identifying phishing attacks. This project implements a complete MLOps pipeline from data ingestion to model deployment with production-ready infrastructure.

![Python](https://img.shields.io/badge/python-v3.10+-blue.svg)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=flat&logo=docker&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-%234ea94b.svg?style=flat&logo=mongodb&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=flat&logo=fastapi)
![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=flat&logo=amazon-aws&logoColor=white)

## 🚀 Features

### 🔧 End-to-End ML Pipeline
- **Automated Data Ingestion**: Import data from CSV files and MongoDB
- **Data Validation**: Comprehensive data quality checks with drift detection
- **Feature Engineering**: Advanced data transformation and preprocessing
- **Model Training**: Automated ML model training with hyperparameter optimization
- **Batch Prediction**: Large-scale prediction capabilities

### 📊 Data Management
- **MongoDB Integration**: Scalable NoSQL database for storing network security data
- **Data Versioning**: Track changes and maintain data lineage
- **Cloud Storage**: AWS S3 integration for artifact storage
- **CSV to JSON Conversion**: Flexible data format handling

### 🌐 Web API & Interface
- **REST API**: FastAPI-based service for real-time predictions
- **Web Interface**: Simple HTML interface for viewing results
- **CORS Support**: Cross-origin resource sharing for web integration
- **File Upload**: Support for uploading security data files

### 🔄 MLOps Infrastructure
- **Docker Containerization**: Consistent deployment environments
- **CI/CD Pipeline**: Automated testing and deployment with GitHub Actions
- **AWS Integration**: ECR for container registry, S3 for storage
- **Comprehensive Logging**: Detailed logging for monitoring and debugging
- **Exception Handling**: Robust error handling framework

## 🏗️ Architecture

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Data Sources  │───▶│  Data Pipeline  │───▶│  ML Pipeline    │
│                 │    │                 │    │                 │
│ • CSV Files     │    │ • Ingestion     │    │ • Training      │
│ • MongoDB       │    │ • Validation    │    │ • Evaluation    │
│ • API Uploads   │    │ • Transform     │    │ • Prediction    │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                                 │                        │
                                 ▼                        ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Monitoring    │    │   Artifacts     │    │  API Service    │
│                 │    │                 │    │                 │
│ • Logging       │    │ • Models        │    │ • FastAPI       │
│ • Drift Det.    │    │ • Data          │    │ • Web UI        │
│ • Metrics       │    │ • Reports       │    │ • Predictions   │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## 🛠️ Tech Stack

- **Backend**: Python 3.10+, FastAPI, Uvicorn
- **Database**: MongoDB with PyMongo
- **ML Libraries**: Scikit-learn, Pandas, NumPy
- **MLOps**: MLflow, DagsHub
- **Cloud**: AWS (S3, ECR), Docker
- **Frontend**: HTML Templates
- **CI/CD**: GitHub Actions
- **Environment**: Python-dotenv

## ⚡ Quick Start

### Prerequisites
- Python 3.10+
- Docker (optional)
- MongoDB instance
- AWS Account (for cloud features)

### 1. Clone Repository
```bash
git clone https://github.com/your-username/networksecurity.git
cd networksecurity
```

### 2. Environment Setup
```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # Linux/Mac
# or
venv\Scripts\activate     # Windows

# Install dependencies
pip install -r requirements.txt
```

### 3. Environment Configuration
Create a `.env` file in the root directory:
```env
MONGO_DB_URL=mongodb://localhost:27017
MONGODB_URL_KEY=mongodb://localhost:27017
AWS_ACCESS_KEY_ID=your_access_key
AWS_SECRET_ACCESS_KEY=your_secret_key
AWS_REGION=us-east-1
```

### 4. Run the Application
```bash
# Start the FastAPI server
python app.py
```

Visit `http://localhost:8000` to access the web interface.

## 📋 Usage

### Data Ingestion
```python
from networksecurity.pipeline.training_pipeline import TrainingPipeline

# Initialize and run training pipeline
pipeline = TrainingPipeline()
pipeline.run_pipeline()
```

### Making Predictions
```python
# Using the API
import requests

response = requests.post(
    "http://localhost:8000/predict",
    files={"file": open("data.csv", "rb")}
)
```

### Batch Processing
```python
# Upload data to MongoDB
python push_data.py
```

## 🐳 Docker Deployment

### Build Image
```bash
docker build -t networksecurity .
```

### Run Container
```bash
docker run -p 8000:8000 --env-file .env networksecurity
```

## ☁️ AWS Deployment

### Setup ECR Repository
```bash
# Create ECR repository
aws ecr create-repository --repository-name networksecurity

# Login to ECR
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin your-account.dkr.ecr.us-east-1.amazonaws.com
```

### Deploy to EC2
```bash
# Update system
sudo apt-get update -y && sudo apt-get upgrade -y

# Install Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu
newgrp docker

# Pull and run container
docker pull your-account.dkr.ecr.us-east-1.amazonaws.com/networksecurity:latest
docker run -d -p 8000:8000 --env-file .env your-account.dkr.ecr.us-east-1.amazonaws.com/networksecurity:latest
```

## 🔧 Configuration

### GitHub Secrets (for CI/CD)
Set the following secrets in your GitHub repository:
- `AWS_ACCESS_KEY_ID`
- `AWS_SECRET_ACCESS_KEY` 
- `AWS_REGION` (e.g., us-east-1)
- `AWS_ECR_LOGIN_URI`
- `ECR_REPOSITORY_NAME`

### MongoDB Configuration
- Default database: `KRISHAI` 
- Collection: `NetworkData`
- Ensure MongoDB is running and accessible

## 📊 Project Structure

```
networksecurity/
├── networksecurity/           # Main application package
│   ├── components/           # ML pipeline components
│   ├── entity/              # Data classes and configurations
│   ├── exception/           # Custom exception handling
│   ├── logging/            # Logging configuration
│   ├── pipeline/           # Training and prediction pipelines
│   ├── utils/              # Utility functions
│   └── cloud/              # AWS integration
├── Network_Data/           # Raw data files
├── Artifacts/             # Generated artifacts
├── final_model/           # Trained models
├── templates/             # HTML templates
├── Dockerfile            # Container configuration
├── requirements.txt      # Python dependencies
├── app.py               # FastAPI application
└── push_data.py         # Data upload utility
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

For support and questions:
- Create an [Issue](https://github.com/your-username/networksecurity/issues)
- Contact: your-email@domain.com

## 🎯 Future Enhancements

- [ ] Real-time streaming data processing
- [ ] Advanced visualization dashboard
- [ ] Model performance monitoring
- [ ] Multi-model ensemble predictions
- [ ] GraphQL API support
- [ ] Kubernetes deployment configurations

---

⭐ **Star this repository if you find it helpful!**