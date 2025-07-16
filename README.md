
# End-to-End Chest Disease Classification with MLflow, DVC & CI/CD Deployment on AWS

## 📦 Project Overview

This project provides a comprehensive end-to-end machine learning pipeline for **chest disease classification** using **MLflow** for experiment tracking, **DVC** for data and pipeline versioning, and **GitHub Actions with AWS** for automated CI/CD deployment.

## ⚙️ Project Workflow

1. Update `config.yaml` with your global settings.
2. Optionally update `secrets.yaml` with API keys or sensitive credentials.
3. Modify `params.yaml` for hyperparameters and runtime configurations.
4. Set or update the `entity` (e.g., your experiment name).
5. Update the `ConfigurationManager` class inside `src/config/`.
6. Refactor or build necessary components (preprocessing, training, etc.).
7. Assemble or modify the pipeline logic.
8. Update the `main.py` script to reflect your new workflow.
9. Modify or recreate `dvc.yaml` to match pipeline stages.

## 🚀 MLflow Setup

- [MLflow Documentation](https://mlflow.org/docs/latest/index.html)  
- [MLflow Tutorial Playlist](https://youtube.com/playlist?list=PLkz_y24mlSJZrqiZ4_cLUiP0CBN5wFmTb)

### Launch MLflow UI

\`\`\`bash
mlflow ui
\`\`\`

### Use MLflow with Dagshub

To run with [Dagshub](https://dagshub.com/):

\`\`\`bash
export MLFLOW_TRACKING_URI=https://dagshub.com/entbappy/chest-Disease-Classification-MLflow-DVC.mlflow
export MLFLOW_TRACKING_USERNAME=entbappy 
export MLFLOW_TRACKING_PASSWORD=6824692c47a369aa6f9353c5b10041d5c8edbcef0

python script.py
\`\`\`

## 📁 DVC Commands

\`\`\`bash
dvc init     # Initialize DVC in the project
dvc repro    # Reproduce pipeline stages
dvc dag      # Visualize the pipeline
\`\`\`

## 🧪 MLflow vs DVC (Quick Comparison)

| Feature                  | MLflow                        | DVC                         |
|--------------------------|-------------------------------|-----------------------------|
| Use-case                 | Production-grade pipelines     | Lightweight POCs            |
| Core focus               | Experiment tracking, registry | Data & pipeline versioning  |
| Model management         | Yes                           | No                          |
| Orchestration support    | Partial                       | Yes                         |
| Ideal for                | Full ML lifecycle             | Quick prototyping           |

## ☁️ CI/CD Deployment on AWS with GitHub Actions

### 1. AWS IAM Setup
- Create an IAM user with:
  - **EC2 full access**
  - **ECR full access**

### 2. Create an ECR Repository
- Example:  
  \`566373416292.dkr.ecr.us-east-1.amazonaws.com/chest-app\`

### 3. Launch EC2 Instance
- Recommended: **Ubuntu Server**

### 4. Install Docker on EC2

\`\`\`bash
sudo apt-get update -y
sudo apt-get upgrade -y
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu
newgrp docker
\`\`\`

### 5. Configure EC2 as Self-hosted GitHub Runner
- Go to: \`GitHub Repo → Settings → Actions → Runners → New Self-hosted Runner\`
- Follow on-screen instructions

### 6. Set GitHub Secrets

| Secret Key              | Value                                       |
|-------------------------|---------------------------------------------|
| \`AWS_ACCESS_KEY_ID\`     | *your access key*                           |
| \`AWS_SECRET_ACCESS_KEY\` | *your secret key*                           |
| \`AWS_REGION\`            | \`us-east-1\` or appropriate region           |
| \`AWS_ECR_LOGIN_URI\`     | \`566373416292.dkr.ecr.us-east-1.amazonaws.com\` |
| \`ECR_REPOSITORY_NAME\`   | \`chest-app\`                                 |

## ✅ Final Notes

- This setup ensures full experiment traceability, lightweight version control, and automatic deployment via CI/CD.
- For production-ready systems, replace placeholder values and rotate credentials periodically.
