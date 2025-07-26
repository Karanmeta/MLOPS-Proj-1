# Proj-1: End-to-End MLOps Pipeline for Vehicle Insurance Claim Prediction

Welcome to **YT-MLops-Proj1**, an advanced, production-grade MLOps pipeline that demonstrates the full lifecycle of machine learning operations! This project transforms raw vehicle insurance data into actionable predictions, predicting whether a customer will file a claim. Built as a tutorial for aspiring ML engineers, it integrates cutting-edge tools for automation, scalability, and reliability—perfect for showcasing your skills to recruiters or collaborators.

From data ingestion in MongoDB to model deployment on AWS via Docker and GitHub Actions, this repo highlights real-world MLOps techniques like CI/CD, cloud orchestration, and robust testing. It's not just a model; it's a complete ecosystem designed for seamless development, deployment, and monitoring.

## 🚀 Project Overview

This pipeline tackles a binary classification problem: predicting the likelihood of vehicle insurance claims based on customer profiles. By leveraging demographic, driving, and vehicle data, it empowers insurers to assess risks, refine pricing, and minimize losses. The end-to-end workflow ensures reproducibility, from exploratory data analysis (EDA) to real-time predictions via a web app.

- **Business Impact**: Enables data-driven decisions in insurance, reducing fraud and optimizing policies.
- **MLOps Focus**: Automates the ML lifecycle to bridge dev and ops, emphasizing scalability, monitoring, and continuous improvement.
- **Key Innovation**: Integrates cloud-native services with containerization for effortless scaling and deployment.


## ✨ Key Features

- **Automated Data Pipeline**: Ingests and validates data from MongoDB, with schema checks and transformation for clean, reliable inputs.
- **Model Training \& Evaluation**: Trains high-accuracy models with hyperparameter tuning, evaluates against thresholds, and pushes superior models to production.
- **Real-Time Predictions**: User-friendly web interface (built with FastAPI) for inputting features and generating instant claim predictions.
- **CI/CD Automation**: GitHub Actions orchestrate builds, tests, and deployments to AWS EC2, ensuring zero-downtime updates.
- **Cloud Scalability**: Leverages AWS S3 for model storage, ECR for Docker images, and EC2 for hosting—ready for high-traffic scenarios.
- **Robust Testing**: Includes unit tests with Pytest, exception handling, and logging for production-level reliability.
- **Extensibility**: Modular components allow easy integration of new models, datasets, or monitoring tools like drift detection.


## 🛠️ Tech Stack \& Techniques

This project employs a modern, enterprise-level stack to exemplify MLOps best practices:

- **Data Storage \& Management**:
    - **MongoDB Atlas**: Cloud-based NoSQL database for scalable data ingestion, storage, and retrieval in key-value format.
    - Custom ingestion scripts for transforming raw datasets into pandas DataFrames.
- **Model Development**:
    - **Python 3.10** with libraries like Scikit-learn for training binary classifiers.
    - Jupyter Notebooks for EDA, feature engineering, and experimentation.
    - Pydantic-inspired entity configs for structured artifacts (e.g., DataIngestionConfig, ModelTrainerArtifact).
- **Automation \& Orchestration**:
    - **Docker**: Containerizes the entire app for consistent environments, from local dev to cloud deployment.
    - **GitHub Actions**: CI/CD workflows for automated testing, building Docker images, and pushing to AWS ECR.
- **Cloud Services**:
    - **AWS Ecosystem**: EC2 for hosting, S3 for model registry (with buckets like "my-model-mlopsproj"), ECR for image repositories, and IAM for secure access management.
    - Environment variable integration for AWS credentials, ensuring secure connections.
- **Testing \& Reliability**:
    - **Pytest**: Comprehensive unit and integration tests for pipelines and endpoints.
    - Custom logging and exception handling modules for debugging and error management.
    - Schema validation with YAML configs to enforce data integrity.
- **Deployment \& Serving**:
    - **FastAPI**: High-performance API for model inference and web app (accessible at routes like /predict and /train).
    - EC2 instance setup with Docker for running the app on port 5080, exposed via public IP.

These techniques ensure the pipeline is **reproducible**, **scalable**, and **production-ready**, incorporating MLOps pillars like versioning, monitoring thresholds (e.g., 0.02 score change for model updates), and asynchronous processing.

## 📊 Model Inputs \& Outputs

- **Inputs** (via Web Form or API):
    - Demographics: Age, gender, education, income, marital status, number of children.
    - Driving History: Experience years, speeding violations, DUIs, past accidents.
    - Vehicle Details: Ownership, year, type (e.g., sedan, sports car), annual mileage.
    - Additional: Credit score, postal code.
- **Outputs**:
    - Binary Prediction: 0 (No Claim) or 1 (Claim Likely), with optional probability scores.
    - Deployed as a web app for interactive use or API calls for integration.


## 🏗️ Installation \& Setup

Follow these steps to get the project running locally or in the cloud. We use a virtual environment for isolation.

1. **Project Initialization**:
    - Run `template.py` to generate the project structure.
    - Configure `setup.py` and `pyproject.toml` for local package imports (details in `crashcourse.txt`).
2. **Virtual Environment**:
    - Create and activate: `conda create -n vehicle python=3.10 -y && conda activate vehicle`.
    - Install dependencies: Add modules to `requirements.txt` and run `pip install -r requirements.txt`.
    - Verify: `pip list`.
3. **MongoDB Setup**:
    - Sign up for MongoDB Atlas, create a cluster (M0 tier), set up user credentials, and allow global access (0.0.0.0/0).
    - Copy the connection string and set as env var: `export MONGODB_URL="mongodb+srv://<user>:<pass>@..."`.
    - In `notebook/mongoDB_demo.ipynb`, push your dataset (from `notebook` folder) to MongoDB.
4. **AWS Configuration**:
    - Create IAM user with AdministratorAccess, generate access keys, and set env vars (e.g., `export AWS_ACCESS_KEY_ID="..."`).
    - Create S3 bucket (`my-model-mlopsproj`) and ECR repo (`vehicleproj`).
    - Update `constants/__init__.py` with keys, region (us-east-1), and thresholds.
5. **Pipeline Components**:
    - Implement data ingestion, validation, transformation, model training, evaluation, and pusher using configs in `entity/`, `components/`, and `configuration/`.
    - Add logging/exception handling and test in `demo.py`.
6. **Prediction App**:
    - Set up `app.py` with FastAPI for routes like /train and /predict.
    - Add `static/` and `templates/` for the web interface.

## 🚀 Deployment with CI/CD

1. **Docker Setup**:
    - Create `Dockerfile` and `.dockerignore` for building the containerized app.
2. **GitHub Actions**:
    - Configure workflows in `.github/workflows/aws.yaml`.
    - Add secrets: AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY, AWS_DEFAULT_REGION, ECR_REPO.
    - Push changes to trigger CI/CD: Builds Docker image, pushes to ECR, and deploys to EC2.
3. **EC2 Hosting**:
    - Launch Ubuntu EC2 instance (t2.medium, 30GB storage).
    - Install Docker: Run setup commands (e.g., `curl -fsSL https://get.docker.com -o get-docker.sh`).
    - Add self-hosted runner via GitHub settings.
    - Expose port 5000 in security groups.
    - Access the app at `<EC2-public-IP>:5000`.

Train models via `/train` or predict at `/predict`. For production, integrate monitoring for drift and retraining.
