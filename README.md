# Node.js Application with Jenkins CI/CD Pipeline

This project is a simple Node.js application deployed using Jenkins as a CI/CD pipeline. The pipeline automates the build, test, Docker image creation, and deployment of the application to an EC2 instance using Docker.

## Table of Contents
- [Project Overview](#project-overview)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Setup Instructions](#setup-instructions)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
- [CI/CD Pipeline](#cicd-pipeline)
- [Usage](#usage)
- [Benefits](#benefits)
- [License](#license)
- [Contact](#contact)

## Project Overview

This project demonstrates a complete CI/CD workflow using Jenkins to deploy a Node.js application. It covers:
- Building a Node.js application.
- Creating and pushing a Docker image to Docker Hub.
- Deploying the application to an AWS EC2 instance.

## Features

- **Automated Build and Deployment**: Uses Jenkins to automate the build and deployment process.
- **Docker Integration**: The app is containerized using Docker for easy deployment.
- **AWS Deployment**: Deploys the app to an AWS EC2 instance using Docker.
- **Versioning**: Docker images are versioned using Jenkins' build number for easy rollbacks.

## Technologies Used

- **Node.js**: A JavaScript runtime environment.
- **Docker**: For containerization.
- **Jenkins**: CI/CD pipeline tool.
- **AWS EC2**: Hosting the deployed Docker container.
- **Git**: Version control system.
  
## Setup Instructions

### Prerequisites

1. **Jenkins** installed and configured with:
   - Git plugin for code checkout.
   - Docker installed on the Jenkins server.
   - `DOCKERHUB_CREDENTIALS` set up in Jenkins as a credential for Docker Hub authentication.
   - `ssh_cred` set up in Jenkins for accessing the EC2 instance via SSH.

2. **AWS EC2 Instance** configured:
   - Docker installed.
   - Security group allowing access to the app's port (in this case, port `1312`).

### Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/AbdallahHesham44/node-Js.git
   cd node-Js
## Project Workflow

Below is a visual representation of the CI/CD workflow for this project:

![Project Workflow](assets/workflow.png)

1. **Code Checkout**: Jenkins pulls the latest code from the GitHub repository's `main` branch.
2. **Build Application**: Jenkins builds the Node.js application to ensure it functions correctly.
3. **Build Docker Image**: Jenkins creates a Docker image of the application.
4. **Login to Docker Hub**: Jenkins authenticates with Docker Hub using stored credentials.
5. **Push Docker Image**: Jenkins pushes the Docker image to Docker Hub, tagging it with the build number.
6. **Deploy to EC2**: Jenkins connects to an AWS EC2 instance via SSH, pulls the latest Docker image, and deploys it.
