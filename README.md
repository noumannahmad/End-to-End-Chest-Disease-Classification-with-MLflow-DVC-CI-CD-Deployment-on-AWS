
# 🧠 End-to-End Chest Cancer Classification with MLflow, DVC & AWS CI/CD

This project demonstrates a full machine learning workflow for **chest cancer classification**, integrating MLflow for experiment tracking, DVC for pipeline/data versioning, and GitHub Actions for automated deployment to AWS infrastructure.

---

## 🔁 Workflow Overview

1. Update `config.yaml` – general settings
2. (Optional) Update `secrets.yaml` – credentials
3. Modify `params.yaml` – hyperparameters
4. Set experiment `entity`
5. Update configuration manager in `src/config`
6. Build or refine pipeline components
7. Assemble pipeline logic
8. Refactor `main.py`
9. Edit or recreate `dvc.yaml` for DVC pipeline stages

---

## 🚀 MLflow Setup


### Run MLflow UI

```bash
mlflow ui
```

### Use with Dagshub

[Dagshub](https://dagshub.com/)

#### Sample Command

```bash
MLFLOW_TRACKING_URI=https://dagshub.com/entbappy/chest-Disease-Classification-MLflow-DVC.mlflow \
MLFLOW_TRACKING_USERNAME=entbappy \
MLFLOW_TRACKING_PASSWORD=6824692c47a4545eac5b10041d5c8edbcef0 \
python script.py
```

#### Set Environment Variables

```bash
export MLFLOW_TRACKING_URI=https://dagshub.com/entbappy/chest-Disease-Classification-MLflow-DVC.mlflow
export MLFLOW_TRACKING_USERNAME=entbappy 
export MLFLOW_TRACKING_PASSWORD=6824692c47a369aa6f9353c5b10041d5c8edbcef0
```

---

## 📁 DVC Commands

```bash
dvc init       # Initialize DVC
dvc repro      # Reproduce pipeline
dvc dag        # Visualize pipeline stages
```

---

## 🔍 MLflow vs. DVC – Quick Comparison

| Feature                | MLflow                         | DVC                            |
|------------------------|--------------------------------|--------------------------------|
| Use-case               | Production-grade ML pipelines  | Lightweight prototyping        |
| Tracks experiments     | ✅                             | ✅                             |
| Pipeline orchestration | ⚠️ Partial                     | ✅                             |
| Model registry         | ✅                             | ❌                             |
| Ideal for              | Deployment, tuning             | Data + pipeline versioning     |

---

## ☁️ AWS CI/CD Deployment via GitHub Actions

### 1. Login to AWS Console

### 2. Create IAM User for Deployment

**Permissions:**
- EC2 (for virtual machine access)
- ECR (for Docker image repository)

**IAM Policies:**
- `AmazonEC2ContainerRegistryFullAccess`
- `AmazonEC2FullAccess`

### 3. Create ECR Repository

- Example URI:  
  `566373416292.dkr.ecr.us-east-1.amazonaws.com/chicken`

### 4. Launch an EC2 Instance (Ubuntu Recommended)

### 5. Install Docker on EC2

```bash
sudo apt-get update -y
sudo apt-get upgrade -y
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu
newgrp docker
```

### 6. Configure EC2 as a Self-Hosted GitHub Runner

- GitHub → Repo Settings → Actions → Runners → New Self-Hosted Runner
- Select OS and follow CLI instructions

### 7. Setup GitHub Secrets

```env
AWS_ACCESS_KEY_ID=your_aws_key
AWS_SECRET_ACCESS_KEY=your_secret_key
AWS_REGION=us-east-1
AWS_ECR_LOGIN_URI=566373416292.dkr.ecr.ap-south-1.amazonaws.com
ECR_REPOSITORY_NAME=simple-app
```

---

## ✅ Summary

- MLflow enables robust experiment tracking and model lifecycle management.
- DVC offers lightweight data/pipeline orchestration and versioning.
- GitHub Actions + AWS delivers a scalable and repeatable CI/CD process for deployment.
