📦 **Strapi Deployment Automation with GitHub Actions & Terraform**
Project Overview

This project demonstrates a full CI/CD pipeline for deploying a Strapi Headless CMS application on AWS EC2 using:

* Docker – containerize Strapi
* GitHub Actions – CI to build and push Docker images
* Terraform – infrastructure as code to provision EC2 and deploy Strapi
* AWS – EC2 instance hosting the application

The goal is to automate deployment so that any code push triggers a Docker image build, which can then be manually deployed to EC2 via Terraform.

Features

* Continuous Integration (CI) – Docker build & push on every push to main branch
* Manual Continuous Deployment (CD) – Terraform workflow deploys updated image to EC2
* Automated EC2 setup – Docker installed & Strapi container launched
* Public access – Strapi admin accessible via EC2 public IP
* Environment variable management – .env file for secure configuration
* Infrastructure as Code – VPC, subnet, security groups, and EC2 managed by Terraform

**Architecture**

GitHub Push
   ↓
GitHub Actions (CI)
   ↓
Docker Hub (image stored)
   ↓
Terraform workflow (manual)
   ↓
EC2 pulls new image & runs Strapi
   ↓
Strapi available on public IP


**Prerequisites**

* AWS account with programmatic access (Access Key & Secret Key)
* GitHub repository
* Docker Hub account
* Terraform installed locally or via GitHub Actions
* SSH key for EC2 access

**Project Setup**
1️⃣ **CI Pipeline (GitHub Actions)**

**File: .github/workflows/ci.yml**

* Runs on push to main
* Builds Docker image
* Pushes to Docker Hub
* Saves image tag as output

  Add GitHub Secrets:

 * DOCKER_USERNAME Eg:noorjahan79
 * DOCKER_PASSWORD  Eg: from dockerhub access token password.

**2 . Continuous Deployment (CD) – Terraform**

Note: Terraform was executed manually in VS Code to provision the EC2 instance and deploy the Dockerized Strapi application.

Steps followed:

Created Terraform configuration (main.tf) including:

* EC2 instance (t3.micro)
* Security Group allowing SSH (22) and Strapi (1337)
* user data to install Docker and run the Strapi container

Initialized Terraform:
* Terraform init
* Terraform plan
* Terraform apply
* Terraform Destroy

# Project Environment Configuration

Create a `.env` file in the root of your project with the following content:

```env
# Server configuration
HOST=0.0.0.0
PORT=1337

# Security keys
APP_KEYS=key1,key2,key3,key4
API_TOKEN_SALT=salt123
ADMIN_JWT_SECRET=adminsecret123
JWT_SECRET=jwtsecret123



Terraform Configuration

Key resources in main.tf:

* VPC, Subnet, Internet Gateway
* Security Group for SSH & Strapi port (1337)
* EC2 instance with user_data launching Docker container

Example snippet:
* docker run -d --name strapi -p 1337:1337 noorjahan79/strapi:${IMAGE_TAG}

5️⃣ Accessing Strapi

Get EC2 public IP from AWS Console

Open browser:http://<EC2_PUBLIC_IP>:1337/admin

Login with admin credentials you set on first run

**Commands used **








  






  
