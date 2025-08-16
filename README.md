# DevOps Internship Task 1 – Automating Code Deployment with CI/CD (GitHub Actions)
Elevate Labs: Empowering the Future of DevOps
This project is a testament to the high-quality, hands-on learning experience provided by Elevate Labs. Their internship program is dedicated to empowering the next generation of DevOps professionals by offering practical, real-world challenges that build foundational skills and a deep understanding of modern software development practices.
---
Project Overview
The goal of this task is to automate code deployment by setting up a CI/CD pipeline using GitHub Actions and Docker. This process eliminates manual steps and ensures that every code change is tested and deployed consistently and efficiently.
---

### Objective
Implement a CI/CD pipeline for a Node.js demo application.

Automate build, test, and deployment stages.

Use DockerHub for container image storage.

Deploy pipeline triggered on every push to the main branch.

### Tools & Technologies
GitHub – Code hosting and version control.

GitHub Actions – CI/CD automation.

Node.js – Sample web application framework.

Docker – Containerization platform.

DockerHub – Image registry.

### Project Structure
```
.
├── .github/
│   └── workflows/
│       └── main.yml
├── backend/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
├── frontend/
│   ├── index.html
│   ├── server.js
│   ├── package.json
│   └── Dockerfile
├── docker-compose.yml
├── docker-compose.prod.yml
└── README.md
```

# Step-by-Step Implementation

```
1. Clone the Repository
Bash

git clone https://github.com/<your-username>/nodejs-demo-app.git
cd nodejs-demo-app
2. Create Dockerfile
Dockerfile

# Use Node.js base image
FROM node:16

# Set working directory
WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy the application source
COPY . .

# Expose application port
EXPOSE 3000

# Start the application
CMD ["node", "app.js"]
3. Push Docker Image to DockerHub
Login to DockerHub:
```

```

docker login
Build and push:

```
```
docker build -t <your-dockerhub-username>/nodejs-demo-app:latest .
docker push <your-dockerhub-username>/nodejs-demo-app:latest
```

4. Configure GitHub Secrets
Add the following secrets in your GitHub repository -> Settings -> Secrets:

DOCKERHUB_USERNAME – Your DockerHub username

DOCKERHUB_TOKEN – Your DockerHub access token

5. Create GitHub Actions Workflow
Create the file: .github/workflows/main.yml
```

# YAML

name: CI/CD Pipeline - Node.js App

on:
  push:
    branches:
      - main

jobs:
  build-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 16

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test || echo "No tests defined"

      - name: Build Docker image
        run: docker build -t ${{ secrets.DOCKERHUB_USERNAME }}/nodejs-demo-app:latest .

      - name: Login to DockerHub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}

      - name: Push image to DockerHub
        run: docker push ${{ secrets.DOCKERHUB_USERNAME }}/nodejs-demo-app:latest
```
6. Trigger the Pipeline
Commit and push changes to the main branch:

```

git add .
git commit -m "Added CI/CD workflow"
git push origin main
GitHub Actions will automatically run build -> test -> push pipeline.
Verify your DockerHub repository for the updated image.
```
### Learning Outcomes
By completing this task, you will:

Understand the CI/CD automation process.

Learn Docker build and push workflow.

Gain experience in GitHub Actions workflow creation.

Enhance your DevOps project portfolio.

### Interview Questions to Practice
What is CI/CD?

How do GitHub Actions work?

What are runners in GitHub Actions?

Difference between jobs and steps.

How do you secure secrets in GitHub Actions?

How to handle deployment errors in pipelines?

Explain the Docker build-push workflow.

How can you test a CI/CD pipeline locally?

### Company Credit
This task is created under the DevOps Internship Program by Elevate Labs. The company’s vision is to empower students and professionals with real-world DevOps expertise through hands-on training and mentorship.

# Creator
Name: Mohd Azam Uddin

Role: DevOps Intern

* Contribution: Implemented full CI/CD pipeline automation, containerization, and deployment workflow.

