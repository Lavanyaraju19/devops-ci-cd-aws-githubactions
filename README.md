# devops-ci-cd-aws-githubactions
CI/CD pipeline using Docker, AWS EC2, and GitHub Actions to automate deployment of a Node.js application.
# devops-ci-cd-aws-githubactions

CI/CD pipeline using Docker, AWS EC2, and GitHub Actions to automate deployment of a Node.js application.

## 🚀 Overview

This project demonstrates a complete CI/CD pipeline where:
- Source code is pushed to GitHub
- GitHub Actions builds a Docker image
- Docker image is pushed to Docker Hub
- AWS EC2 instance pulls the image and runs the container

## 🧰 Tools & Technologies

- **GitHub Actions** – CI/CD automation
- **Docker** – Containerization
- **AWS EC2** – Hosting environment
- **Node.js** – Sample application
- **Nginx** – Reverse proxy (optional)

## 🛠️ Project Structure
 ├── .github/workflows/ # GitHub Actions workflows ├── app/ # Node.js application │ └── Dockerfile # Docker image definition ├── deploy.sh # EC2 deployment script └── README.md

## ⚙️ How It Works

1. Developer pushes code to `main` branch
2. GitHub Action:
   - Builds Docker image
   - Pushes to Docker Hub
   - SSHes into EC2 and runs deployment script
3. App is deployed via Docker container on EC2

## 🔐 Prerequisites

- AWS EC2 instance with Docker & SSH access
- GitHub repository secrets:
  - `EC2_HOST`, `EC2_USER`, `EC2_KEY`
  - `DOCKER_USERNAME`, `DOCKER_PASSWORD`

## 🧪 Run Locally

```bash
cd app
docker build -t your-image-name .
docker run -p 3000:3000 your-image-name

#!/bin/bash
docker pull your-image-name
docker stop my-app || true
docker rm my-app || true
docker run -d --name my-app -p 80:3000 your-image-name
   .github/workflows/deploy.yml

name: Deploy to AWS EC2

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    ...
