# SeoGram – Docker & Jenkins CI/CD Deployment

This project demonstrates the deployment of a static **SeoGram website** using **Docker, Docker Compose, Jenkins, Docker Hub, and AWS EC2**.

The website was taken from a free CSS/template source, uploaded to GitHub, containerized using Docker, tested locally, and then automated using Jenkins for deployment to an AWS EC2 instance.

## 🚀 Tech Stack

* HTML / CSS / JavaScript
* Git & GitHub
* Docker
* Docker Compose
* Nginx
* Jenkins
* Docker Hub
* AWS EC2
* Jenkins Agent (Node)

## 🔄 Deployment Flow

```text
Free CSS Template
       ↓
   GitHub Repository
       ↓
     Dockerfile
       ↓
   Docker Image
       ↓
 Docker Compose
       ↓
 Local Deployment
       ↓
     Jenkins
       ↓
 Jenkins Node/Agent
       ↓
 Docker Build
       ↓
 Docker Hub
       ↓
 AWS EC2
       ↓
 Running Website
```

## 📁 Project Structure

```text
seogram-1.0.0/
│
├── assets/
├── html/
├── Dockerfile
├── docker-compose.yml
├── Jenkinsfile
├── Credits.txt
└── LICENSE.txt
```

## 🐳 Docker

The website is packaged into an Nginx Docker image.

The `Dockerfile` uses the latest Nginx image and copies the website's `html` and `assets` directories into the Nginx web root.

Build the image:

```bash
docker build -t seogram:latest .
```

Run the container:

```bash
docker run -d -p 8000:80 --name seogram seogram:latest
```

The website can then be accessed at:

```text
http://localhost:8000
```

## 🐋 Docker Compose

Docker Compose is used to simplify container deployment.

The current Compose configuration runs the `dexter001/seogram:latest` image and maps:

```text
8000:80
```

It also uses `restart: unless-stopped`.

Run:

```bash
docker compose up -d
```

Stop:

```bash
docker compose down
```

## 🔧 Jenkins CI/CD

Jenkins is used to automate the complete deployment process.

The Jenkins pipeline contains the following stages:

### 1. Clone

Jenkins clones the project from GitHub.

### 2. Build

The Docker image is built:

```bash
docker build -t seogram:latest ./seogram-1.0.0
```

### 3. Push

The image is tagged and pushed to Docker Hub:

```text
dexter001/seogram:latest
```

Docker Hub credentials are stored securely in Jenkins credentials rather than being written directly into the pipeline.

### 4. Deploy

Jenkins pulls the latest image and starts the application using Docker Compose:

```bash
docker compose pull
docker compose up -d
```

### 5. Notification

Jenkins sends an email notification after a successful or failed build.

## 🖥️ Jenkins Node / Agent

A separate Jenkins node/agent was configured to perform the Docker and deployment operations.

The pipeline uses the Jenkins agent with the label:

```text
dev
```

This allows the Jenkins controller to delegate the build and deployment work to the configured agent.

## ☁️ AWS EC2 Deployment

After successfully testing the application locally, the deployment was moved to an **AWS EC2 instance**.

The EC2 instance was configured with the required Docker and Jenkins-agent environment.

The deployment process is:

```text
GitHub
   ↓
Jenkins
   ↓
Jenkins Agent
   ↓
Docker Build
   ↓
Docker Hub
   ↓
EC2
   ↓
Docker Compose
   ↓
Nginx Container
   ↓
Website
```

This makes it possible to deploy a new version by triggering the Jenkins pipeline instead of manually copying website files to the server.

## 🧪 Local Testing

Before deploying to EC2, the application was tested locally using Docker and Docker Compose.

```bash
docker compose up -d
```

Then open:

```text
http://localhost:8000
```

Check running containers:

```bash
docker ps
```

View logs:

```bash
docker logs seogram
```

## 🔁 CI/CD Workflow

Whenever the project is updated, Jenkins can execute the following workflow:

```text
Developer Push
      ↓
    GitHub
      ↓
    Jenkins
      ↓
    Clone Code
      ↓
 Docker Image Build
      ↓
 Docker Hub Push
      ↓
   EC2 Server
      ↓
 Docker Compose Pull
      ↓
 Container Restart
      ↓
 Updated Website
```

## 🎯 Project Objective

The main objective of this project was to understand and implement a basic **CI/CD pipeline for a containerized web application**.

Through this project, I worked with:

* Git/GitHub source control
* Docker containerization
* Nginx web server
* Docker Compose
* Jenkins pipelines
* Jenkins agents/nodes
* Docker Hub image management
* AWS EC2 deployment
* Automated application deployment

## 📌 Repository

GitHub:

[View the project on GitHub](https://github.com/devashish-pandey/test-project/tree/main/seogram-1.0.0?utm_source=chatgpt.com)

## 👨‍💻 Author

**Devashish Pandey**

This project was created as a hands-on DevOps/CI-CD implementation using a static website and modern containerized deployment practices.
