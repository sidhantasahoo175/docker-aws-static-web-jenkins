# 🚀 DevOps Static Web Application – CI/CD Deployment

## 📌 Project Overview

This project demonstrates a complete **DevOps CI/CD workflow** for deploying a static web application using **GitHub, Jenkins, Docker, Docker Hub, and AWS EC2**.

The application is developed using HTML5 and CSS3, packaged inside a Docker container using Nginx, automatically built and tested through Jenkins, pushed to Docker Hub, and finally deployed on an AWS EC2 Linux server.

### 🔄 Deployment Flow

**Developer → GitHub → Jenkins → Docker Build → Test → Docker Hub → AWS EC2 → Production**

---

## 🏗️ How the Application Is Built

The application is a static web dashboard created using:

- HTML5 – Application structure
- CSS3 – Styling and responsive design
- Nginx – Web server used to serve the static files
- Docker – Packages the application into a container

The `Dockerfile` uses the lightweight **Nginx Alpine image** and copies the `index.html` file into the Nginx web directory.

The application is exposed through port **80 inside the container**.

---

## 🛠️ Technologies Used

| Technology | Purpose | Where It Is Used |
|---|---|---|
| HTML5 | Creates the application structure | `index.html` |
| CSS3 | Provides styling and responsive UI | `index.html` |
| Nginx | Serves the static website | Docker container |
| Docker | Packages and runs the application | `Dockerfile` |
| Docker Hub | Stores Docker images | Docker image repository |
| Git | Version control | Local project |
| GitHub | Stores source code | GitHub repository |
| Jenkins | Automates CI/CD pipeline | `Jenkinsfile` |
| AWS EC2 | Hosts the production application | EC2 instance |
| Linux | Server operating system | AWS EC2 |
| PowerShell | Used for local project and Git commands | Windows development machine |

---

## 🔄 CI/CD Pipeline

The Jenkins pipeline is defined inside the `Jenkinsfile`.

### 1️⃣ Build Docker Image

Jenkins builds the Docker image from the project `Dockerfile`.

```text
docker build

Two image tags are created:

Build number
latest
2️⃣ Test Container

After building the image, Jenkins starts a temporary container on port 8081.

Jenkins then checks whether the application is responding successfully.

http://localhost:8081/

If the application responds successfully, the temporary container is removed.

3️⃣ Push to Docker Hub

Jenkins authenticates with Docker Hub using stored Jenkins credentials.

The Docker image is then pushed to:

siddh342/docker-aws-static-web

Both the build-number tag and latest tag are pushed.

4️⃣ Deploy to AWS EC2

Jenkins connects to the Docker environment running on the EC2 server.

The previous application container is removed and the latest Docker image is pulled from Docker Hub.

A new container is then started:

Docker Container Port 80
        ↓
EC2 Port 8000

The application becomes available through:

http://13.127.123.179:8000
📦 Docker Configuration

The project uses the following Dockerfile:

FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
Dockerfile Explanation
Instruction	Purpose
FROM nginx:alpine	Uses lightweight Nginx image
COPY	Copies the application into Nginx web directory
EXPOSE 80	Documents the container web port
CMD	Starts Nginx in the foreground
⚙️ Jenkins Pipeline Stages

The Jenkinsfile contains the following stages:

1. Build Docker Image
        ↓
2. Test Container
        ↓
3. Push to Docker Hub
        ↓
4. Deploy to AWS EC2
Jenkins Responsibilities

Jenkins automatically:

Retrieves the latest source code from GitHub
Builds the Docker image
Runs an application test
Pushes the image to Docker Hub
Pulls the latest image
Deploys the application container on AWS EC2
☁️ AWS EC2 Deployment

The production environment runs on an Amazon EC2 Linux server.

Docker and Jenkins are installed on the EC2 instance.

The application runs inside a Docker container:

AWS EC2
   │
   ├── Jenkins
   │
   └── Docker
        │
        └── Static Web Container
              │
              └── Nginx
                   │
                   └── index.html

The application is exposed using:

EC2 Port 8000 → Docker Port 80
🔐 Credentials and Security

Sensitive credentials are not stored inside the source code.

The project uses:

Jenkins Credentials for Docker Hub authentication
Jenkins Credentials for GitHub authentication
.gitignore to prevent the EC2 .pem key from being committed

The EC2 private key file is intentionally excluded from GitHub.

🎯 Key DevOps Concepts Demonstrated

This project demonstrates practical knowledge of:

Version Control
Git & GitHub
Continuous Integration
Continuous Deployment
Jenkins Pipeline
Docker Containerization
Docker Image Management
Docker Hub
Linux Server Administration
AWS EC2
Nginx
Automated Testing
Environment Deployment
CI/CD Automation
💡 Interview Quick Hints
❓ Why did you use Docker?

Answer:
I used Docker to package the application and its web server into a portable container so that the application can run consistently across different environments.

❓ Why did you use Jenkins?

Answer:
Jenkins automates my CI/CD process. It builds the Docker image, tests the application, pushes the image to Docker Hub, and deploys the latest image to AWS EC2.

❓ Why Docker Hub?

Answer:
Docker Hub is used as a centralized registry to store and manage the Docker images generated by the Jenkins pipeline.

❓ Why AWS EC2?

Answer:
AWS EC2 provides the Linux server environment where Docker, Jenkins, and the production application container are running.

❓ Why Nginx?

Answer:
Nginx is used as the web server inside the Docker container to serve the static HTML application.

❓ What happens when you change the application?

Answer:
I commit and push the changes to GitHub. Jenkins retrieves the updated code, builds a new Docker image, tests it, pushes it to Docker Hub, and deploys the latest image on AWS EC2.

❓ What is the complete CI/CD flow?

Answer:

GitHub
   ↓
Jenkins
   ↓
Docker Build
   ↓
Application Test
   ↓
Docker Hub
   ↓
AWS EC2
   ↓
Docker Container
   ↓
Nginx
   ↓
Live Application
📁 Project Structure
docker-aws-static-web-jenkins/
│
├── screenshots/
│
├── .dockerignore
├── .gitignore
├── Dockerfile
├── Jenkinsfile
├── README.md
└── index.html
📸 Project Screenshots
🌐 Live Application

🔨 Jenkins Successful Build

🐳 Docker Hub

☁️ AWS EC2

📂 GitHub Repository

Note: Make sure the screenshot filenames inside your screenshots folder exactly match the names used above.

🌐 Live Demo

Application:
http://13.127.123.179:8000

📂 GitHub Repository

Repository:
https://github.com/sidhantasahoo175/docker-aws-static-web-jenkins

👨‍💻 Project Summary

This project demonstrates how a static web application can be containerized using Docker and deployed through a CI/CD pipeline.

GitHub is used for source-code management, Jenkins automates the CI/CD process, Docker packages the application, Docker Hub stores the container image, and AWS EC2 provides the production server.

The complete workflow reduces manual deployment steps and demonstrates a practical implementation of modern DevOps practices.
