# Hello Jenkins Demo 🚀

A simple Spring Boot application demonstrating a fully automated CI/CD pipeline using **GitHub, Jenkins, Docker, AWS ECR, and AWS EC2**.

## Tech Stack

- Java 21
- Spring Boot 4.0.7
- Maven
- Jenkins
- Docker
- AWS ECR
- AWS EC2
- GitHub

## Application

The application is a simple Spring Boot REST API running on port `8081`.

### Endpoint

```http
GET /
```

Response:

```text
Hello from Fully Automated CI/CD Pipeline!
```

## Project Structure

```text
hello_jenkins_demo/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── ...
│   │   └── resources/
│   │       └── application.properties
│   └── test/
│       └── ...
├── Dockerfile
├── Jenkinsfile
├── pom.xml
├── mvnw
├── mvnw.cmd
└── README.md
```

## How the CI/CD Pipeline Works

```text
Developer
    │
    │ git push
    ▼
GitHub
    │
    ▼
Jenkins
    │
    ├── Checkout Code
    │
    ├── Build Maven Project
    │
    ├── Build Docker Image
    │
    ├── Push Docker Image
    │
    ▼
AWS ECR
    │
    │ Docker image
    ▼
AWS EC2
    │
    ├── Pull latest image
    ├── Stop old container
    ├── Remove old container
    └── Start new container
    │
    ▼
Spring Boot Application
    │
    └── Port 8081
```

### Pipeline Flow

1. Code is pushed to GitHub.
2. Jenkins checks out the latest source code.
3. Jenkins builds the Spring Boot application using Maven.
4. Jenkins creates a Docker image.
5. Jenkins authenticates with AWS ECR.
6. Jenkins pushes the Docker image to the ECR repository.
7. Jenkins connects to the AWS EC2 instance through SSH.
8. EC2 authenticates with ECR and pulls the latest image.
9. The previous `hello-app` container is stopped and removed.
10. A new container is started using the latest image.
11. The application becomes available on port `8081`.

## Local Setup

### Clone the repository

```bash
git clone <your-repository-url>
cd hello_jenkins_demo
```

### Build the project

Using Maven Wrapper:

```bash
./mvnw clean package
```

On Windows:

```powershell
.\mvnw.cmd clean package
```

### Run locally

```bash
./mvnw spring-boot:run
```

On Windows:

```powershell
.\mvnw.cmd spring-boot:run
```

The application runs on:

```text
http://localhost:8081
```

## Docker

Build the application first:

```bash
./mvnw clean package
```

Build the Docker image:

```bash
docker build -t hello-app:latest .
```

Run the container:

```bash
docker run -d --name hello-app -p 8081:8081 hello-app:latest
```

Then open:

```text
http://localhost:8081/
```

## Jenkins Pipeline

The `Jenkinsfile` contains the following stages:

```text
Checkout Code
      ↓
Build Maven Project
      ↓
Build Docker Image
      ↓
Push Docker Image to AWS ECR
      ↓
Deploy to AWS EC2
```

Jenkins is responsible for automating the complete build, image creation, image publishing, and deployment process.

## AWS Components

### Amazon ECR

The Docker image is pushed to an Amazon ECR repository:

```text
hello-app
```

The configured AWS region is:

```text
ap-south-1
```

### Amazon EC2

The EC2 instance runs the Docker container containing the Spring Boot application.

The container uses:

```text
8081:8081
```

so port `8081` of the EC2 instance maps to port `8081` inside the container.

## Docker Image Lifecycle

```text
Spring Boot JAR
      ↓
Docker Image
      ↓
AWS ECR
      ↓
AWS EC2
      ↓
Docker Container
      ↓
Spring Boot Application
```

## Purpose of This Project

This project is a **CI/CD demonstration project**.

The main objective is to understand how application code can automatically move from:

```text
GitHub → Jenkins → Docker → AWS ECR → AWS EC2
```

after a code change.

It is intentionally kept simple so the CI/CD workflow can be understood clearly.

## Future Improvements

Possible improvements for a production-oriented pipeline include:

- Jenkins Credentials instead of hardcoded deployment values
- Maven Wrapper in the Jenkins build stage
- Post-deployment health check
- Docker image cleanup
- Versioned Docker image tags
- Rollback strategy
- HTTPS
- Monitoring and logging

These are outside the scope of this basic demo.

## Status

**Demo CI/CD Pipeline: Complete ✅**

The project demonstrates automated:

- Source checkout
- Maven build
- Docker image creation
- ECR image push
- EC2 deployment