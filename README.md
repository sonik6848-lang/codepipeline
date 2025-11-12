# 🚀 AWS CodeBuild – Docker Image Push to Amazon ECR

This project automates the process of building and pushing Docker images to **Amazon Elastic Container Registry (ECR)** using **AWS CodeBuild**.  
It includes a `Dockerfile` for image creation and a `buildspec.yml` configuration for defining the build pipeline.

---

## 📦 Project Overview

The primary goal of this project is to enable **continuous integration (CI)** with AWS CodeBuild.  
Whenever CodeBuild runs (manually or via a pipeline trigger), it will:

1. Build a Docker image using the provided `Dockerfile`.
2. Tag the image with a version or build ID.
3. Authenticate with Amazon ECR.
4. Push the Docker image to your specified ECR repository.

---

## 🧩 Files Included

| File | Description |
|------|--------------|
| `Dockerfile` | Defines the Docker image structure and dependencies. |
| `buildspec.yml` | AWS CodeBuild configuration file containing all build commands and ECR push steps. |

---

## ⚙️ Prerequisites

Before you run this project, make sure you have:

- An **AWS account** with access to CodeBuild, ECR, and IAM permissions.  
- An existing **ECR repository** created in your AWS account.  
- **AWS CLI** installed and configured locally (for testing).  
- **Docker** installed and running on your system (optional for local testing).  

---

## 🧱 How It Works

1. **CodeBuild Setup**
   - Create a new CodeBuild project in the AWS Console.
   - Connect your source repository (GitHub, CodeCommit, Bitbucket, etc.).
   - Use the `buildspec.yml` file included in this repo.
   - Set environment variables such as:
     - `AWS_DEFAULT_REGION`
     - `ECR_REPO_URI`
     - `IMAGE_TAG` (optional, defaults to `latest`)

2. **Build Steps**
   The `buildspec.yml` handles the following steps:
   - Login to ECR
   - Build Docker image using the `Dockerfile`
   - Tag the image
   - Push the image to your ECR repository

3. **Output**
   After the build completes successfully, your Docker image will be available in **ECR** with the defined tag.

---

## 🧪 Local Testing (Optional)

If you want to test locally before CodeBuild:

```bash
# Build Docker image
docker build -t my-app .

# Tag image for ECR
docker tag my-app:latest <aws_account_id>.dkr.ecr.<region>.amazonaws.com/<repository_name>:latest

# Login to ECR
aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.<region>.amazonaws.com

# Push image
docker push <aws_account_id>.dkr.ecr.<region>.amazonaws.com/<repository_name>:latest
