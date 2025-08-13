# Simple User Signup & Login Application

### Introduction

Welcome to this full-stack user authentication application. This project was built from the ground up to serve as a practical example of a secure, modern web application. It features a Python backend powered by the Flask framework and a dynamic, user-friendly frontend built with standard HTML, CSS, and JavaScript.

**Project created by Mohd Azam Uddin.**

---
## What is this App?

This application provides a fundamental user authentication system. Its core purpose is to allow new users to create a secure account and for existing users to sign in. It serves as a solid foundation for any web application that requires user management.

**Key Features:**
* Secure user registration with password hashing.
* User login and a personalized welcome dashboard.
* A clean, responsive user interface.

---
## How It Was Built - The Journey

This project started with a simple goal: create a functional signup system. The process evolved as we tackled common development challenges.

#### 1. The Initial Backend
The first version of the application was a simple **Flask** server, storing user data in a `users.json` file. This approach quickly led to an **"Internal Server Error"** due to file permission issues and the risk of data corruption.

#### 2. Upgrading to a Real Database
To fix the errors and make the application more stable, the backend was upgraded to use a proper **SQLite** database. The `Flask-SQLAlchemy` library was used to manage the database, which solved all the data storage problems.

#### 3. Building the Frontend
The user interface was built with standard **HTML**, **CSS**, and **vanilla JavaScript**. A simple **Node.js/Express** server is used to serve the `index.html` file and manage the local development environment.

---
## Containerization with Docker

To ensure the application runs reliably in any environment, it has been fully containerized using Docker.

#### What is Containerization?
Imagine a standardized shipping container that holds not just your application's code, but also the specific version of Python or Node.js it needs, all the required libraries, and the necessary system settings. This "box" can be run on any machine that has Docker installed, guaranteeing that the app will work the same way for a developer, a tester, or in a production environment. This solves the classic "it works on my machine" problem.

#### Creating the Dockerfiles
A `Dockerfile` is a blueprint for building a container image. This project uses two separate `Dockerfile`s for the backend and frontend, which detail the steps to package each service.

---
## Automation with GitHub Actions CI/CD

This project uses a fully automated CI/CD (Continuous Integration/Continuous Deployment) pipeline built with GitHub Actions.

#### What is CI/CD and Why Use It?
CI/CD is a modern software development practice that automates the process of building, testing, and deploying code.
* **Continuous Integration (CI)** automatically tests the code every time a change is pushed. This catches bugs early and ensures that new code doesn't break existing features.
* **Continuous Deployment (CD)** automatically builds the application and deploys it after it passes all the tests.

We use this to save time, reduce human error, and ensure that only high-quality, tested code makes it to production.

#### How the Pipeline Was Built
The entire pipeline is defined in a single YAML file located at `.github/workflows/main.yml`. This file contains all the instructions for the automated workflow.

#### The Pipeline's Workflow: Step-by-Step
When code is pushed to the `main` branch, the following happens automatically:
1.  **Trigger**: The `push` event automatically starts the pipeline.
2.  **Test Job**: This job runs first to ensure code quality.
    * It checks out the latest code.
    * It sets up separate Python and Node.js environments.
    * It runs the command `pip install -r requirements.txt` to install backend dependencies.
    * It runs `flake8 .` to lint the Python code for errors.
    * It runs `npm ci` to install frontend dependencies.
    * It runs `npx eslint .` to lint the JavaScript code.
3.  **Build & Push Job**: This job only runs if the `test` job succeeds.
    * It securely logs into Docker Hub.
    * It runs the `docker build` command to create new images for the backend and frontend.
    * It runs the `docker push` command to upload the new images to Docker Hub, tagging them as `:latest`.

#### Secrets and Variables
To log in to Docker Hub securely, the pipeline uses encrypted secrets stored in the GitHub repository's settings (`Settings > Secrets and variables > Actions`).
* **`DOCKERHUB_USERNAME`**: Stores the Docker Hub username.
* **`DOCKERHUB_TOKEN`**: Stores a secure Docker Hub Access Token used as a password.

---
## Technologies & Dependencies Used

* **Backend**: Python, Flask, Flask-SQLAlchemy, Flask-CORS, Gunicorn
* **Frontend**: HTML5, CSS3, Vanilla JavaScript, Node.js, Express.js
* **Containerization**: Docker, Docker Compose
* **CI/CD**: Docker Image, GitHub Actions

---
## How to Run Locally

The recommended way to run this application is with Docker Compose, as it handles both the frontend and backend setup automatically.

1.  Clone this repository.
2.  Ensure Docker and Docker Compose are installed and running.
3.  From the project's root directory, run the command:
    ```bash
    docker-compose up --build
    ```
4.  Access the application in your web browser at `http://localhost:3000`.

---
## Final Project Structure
```
.
├── .github/
│   └── workflows/
│       └── main.yml
├── backend/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
└── frontend/
    ├── index.html
    ├── server.js
    ├── package.json
    └── Dockerfile
├── docker-compose.yml
├── docker-compose.prod.yml
└── README.md
```