# EduApplication

## Overview

EduApplication is a Flask-based educational platform that allows users to access programming and cloud courses while tracking learning progress.
The platform supports multiple course categories including **C, C++, Java, Python, AWS, and Azure**.

The application also includes **file uploads, user authentication, course tracking, and analytics**.
For DevOps practices, the project is containerized using **Docker** and automated using **Jenkins CI/CD**.

---

# Features

* User Registration and Login
* Course Modules for Programming Languages
* Cloud Courses (AWS & Azure)
* User Progress Tracking
* File Upload System
* Analytics Storage
* Docker Containerization
* Jenkins CI/CD Automation

---

# Tech Stack

### Backend

* Python
* Flask

### Frontend

* HTML
* CSS
* JavaScript

### DevOps

* Docker
* Jenkins
* GitHub

### Server

* Gunicorn

---

# Project Structure

```bash
Eduapplication/
│
├── app.py
├── requirements.txt
├── Dockerfile
├── Jenkinsfile
├── README.md
│
├── templates/
│   ├── login.html
│   ├── register.html
│   ├── welcome.html
│   ├── courses.html
│   ├── uploads.html
│   ├── superuser_dashboard.html
│   └── course pages
│
├── static/
│   ├── css
│   ├── js
│   └── assets
│
├── c_courses/
├── cpp_courses/
├── java_courses/
├── python_courses/
│
├── ai_analytics.json
├── student_progress.json
├── student_timetables.json
├── user_profiles.json
├── user_courses.txt
├── users.txt
```

---

# Storage System

This project uses **JSON and text-based storage instead of a database**.

### User Accounts

Stored in:

```
users.txt
```

Contains registered users.

---

### User Profiles

Stored in:

```
user_profiles.json
```

Stores profile information of users.

---

### Course Progress

Stored in:

```
student_progress.json
```

Tracks the progress of each student in different courses.

---

### Timetable Data

Stored in:

```
student_timetables.json
```

Stores student schedules.

---

### AI Analytics

Stored in:

```
ai_analytics.json
```

Stores analytics and course insights.

---

# Running the Project Locally

### 1 Clone Repository

```bash
git clone https://github.com/VarshithChand/Eduapplication.git
```

### 2 Navigate to Project

```bash
cd Eduapplication
```

### 3 Install Dependencies

```bash
pip install -r requirements.txt
```

### 4 Run Application

```bash
python app.py
```

Application runs on

```
http://localhost:5000
```

---

# Docker Setup

### Build Docker Image

```bash
docker build -t eduvault .
```

---

### Run Container

```bash
docker run -p 5000:5000 eduvault
```

Open browser

```
http://localhost:5000
```

---

# Dockerfile

```dockerfile
FROM python:3.10

WORKDIR /app

COPY . .

RUN pip install -r requirements.txt

EXPOSE 5000

CMD ["gunicorn","--bind","0.0.0.0:5000","app:app"]
```

---

# Jenkins CI/CD Pipeline

Jenkins automatically:

1. Pulls latest code from GitHub
2. Builds Docker image
3. Runs container

---

# Jenkinsfile

```groovy
pipeline {
    agent any

    environment {
        IMAGE_NAME = "eduvault"
    }

    stages {

        stage('Clone Repository') {
            steps {
                git 'https://github.com/VarshithChand/Eduapplication.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 5000:5000 $IMAGE_NAME:latest'
            }
        }
    }
}
```

---

# DevOps Workflow

```
Developer
   ↓
GitHub Repository
   ↓
Jenkins CI/CD
   ↓
Docker Build
   ↓
Docker Container
   ↓
Flask Web Application
```

---

# Future Improvements

* Database integration (MongoDB / MySQL)
* User role management
* Cloud deployment (AWS / Azure)
* Kubernetes orchestration
* Advanced AI analytics

---

# Author

Varshith Chand

GitHub
https://github.com/VarshithChand

---

# License

This project is licensed under the MIT License.
