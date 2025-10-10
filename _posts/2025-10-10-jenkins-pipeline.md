---
layout: post
title: "Jenkins Pipeline Basics"
date: 2025-10-05
---

Jenkins is one of the most powerful tools for automating software builds, tests, and deployments.  
In this post, we’ll explore how Jenkins Pipelines help create end-to-end CI/CD workflows.

---

🧩 1️⃣ What is Jenkins

Jenkins is an open-source automation server used for Continuous Integration (CI) and Continuous Deployment (CD).
It automates the entire software development lifecycle — from code build, test, deployment, to monitoring.

Developers commit code → Jenkins builds, tests, and deploys automatically.

Main Purpose: Reduce manual work and errors in the deployment process.



---

⚙️ 2️⃣ Jenkins Architecture

Components:

1. Jenkins Master (Controller):

Controls the pipeline, schedules builds, monitors agents.



2. Jenkins Agent (Slave):

Executes the actual build/test/deploy steps.



3. Build Executor:

The unit inside an agent that performs the job.




Example:
You may have one master node and multiple agent nodes (Linux/Windows) handling various environments — Dev, QA, Prod.


---

🧱 3️⃣ Jenkins Installation

🖥️ On Linux:

sudo apt update
sudo apt install openjdk-17-jdk -y
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt install jenkins -y
sudo systemctl start jenkins
sudo systemctl enable jenkins

Access Jenkins → http://<server_ip>:8080
Default password:
sudo cat /var/lib/jenkins/secrets/initialAdminPassword


---

🧰 4️⃣ Jenkins Basics

Common Terms:

Job: A task (build/test/deploy)

Build: Execution of a job

Plugin: Adds extra functionality (e.g., Git, Docker, Slack)

Workspace: Directory where Jenkins runs builds

Node: Machine Jenkins runs on



---

🧾 5️⃣ Jenkins Job Types

1. Freestyle Project → GUI-based setup for small/simple tasks


2. Pipeline Project → Written in code (Jenkinsfile)


3. Multibranch Pipeline → For multiple Git branches


4. Folder → Organize jobs


5. External Job → Trigger jobs from outside Jenkins




---

🧪 6️⃣ Jenkins with Git

Steps:

1. Install Git Plugin


2. Create a new job → Select “Git” under SCM


3. Enter repo URL → Choose branch


4. Add build steps like:

Compile code

Run tests

Deploy




Example: Fetch code → build → run tests


---

🧩 7️⃣ Jenkins Pipeline (Declarative Syntax)

Example Jenkinsfile

pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/dheeraj/example-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                sh 'ansible-playbook deploy.yml'
            }
        }
    }
}

Explanation:

Pulls code from Git

Builds using Maven

Runs tests

Deploys with Ansible



---

🚀 8️⃣ Jenkinsfile (Scripted Pipeline)

node {
    stage('Checkout') {
        git 'https://github.com/dheeraj/example-app.git'
    }
    stage('Build') {
        sh 'mvn clean package'
    }
    stage('Test') {
        sh 'mvn test'
    }
    stage('Deploy') {
        sh 'ansible-playbook deploy.yml'
    }
}

Scripted pipelines use Groovy scripting for more flexibility and logic-based flows.


---

🧩 9️⃣ Integration with DevOps Tools

Tool	Integration Purpose

GitHub / GitLab / Bitbucket	SCM Integration (webhooks)
Maven / Gradle	Build tools
SonarQube	Code quality
Docker	Container build & push
Kubernetes	Deployment automation
Ansible / Terraform	Configuration & Infrastructure automation
Slack / Email	Notifications



---

🧱 🔟 Jenkins Pipeline Example with Docker & Kubernetes

pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/dheeraj/myapp.git'
      }
    }
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t myapp:latest .'
      }
    }
    stage('Push to DockerHub') {
      steps {
        withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_HUB_TOKEN')]) {
          sh 'docker login -u dheeraj -p $DOCKER_HUB_TOKEN'
          sh 'docker push dheeraj/myapp:latest'
        }
      }
    }
    stage('Deploy to K8s') {
      steps {
        sh 'kubectl apply -f deployment.yaml'
      }
    }
  }
}

This pipeline builds a Docker image, pushes it to DockerHub, and deploys to Kubernetes.


---

🔐 1️⃣1️⃣ Jenkins Security Best Practices

Create non-root Jenkins user

Use Role-Based Access Control (RBAC) plugin

Integrate with LDAP or Active Directory

Always use credentials plugin for secrets

Regularly back up JENKINS_HOME



---

🧠 1️⃣2️⃣ Advanced Jenkins Concepts

Parameterized Builds: Pass variables dynamically (branch, environment)

Parallel Stages: Run multiple tasks simultaneously

Shared Libraries: Reuse pipeline code across projects

Blue Ocean Plugin: Modern UI for pipelines

Pipeline as Code (PaC): Store Jenkinsfile in repo

Jenkins Shared Libraries Example:

@Library('my-shared-lib') _
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                buildApp()
            }
        }
    }
}



---

📊 1️⃣3️⃣ Jenkins Monitoring and Logs

Build Logs (per job)

System Logs (/var/log/jenkins/jenkins.log)

Integrate with Prometheus Plugin + Grafana dashboards



---

💡 1️⃣4️⃣ Jenkins Interview Key Topics

What is CI/CD?

Difference between Freestyle and Pipeline job

Declarative vs Scripted Pipeline

Jenkins architecture

Jenkinsfile stages and syntax

Integrations (Git, Docker, K8s, Ansible)

How to trigger Jenkins job automatically (webhooks)

Role of Jenkins in DevOps lifecycle



---


