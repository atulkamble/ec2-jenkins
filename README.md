## 🔹 Jenkins

### 🔹 What is Jenkins?

* Open-source **Automation Server**
* Used for **CI/CD (Continuous Integration & Continuous Deployment)**
* Written in **Java**
* Supports **plugins-based architecture**
* Runs as **standalone (WAR), service, Docker container**

---

## 🔹 Core Concepts

### 🔹 CI (Continuous Integration)

* Developers push code to Git
* Jenkins automatically:

  * Pulls code
  * Builds
  * Tests
  * Generates reports

### 🔹 CD (Continuous Delivery/Deployment)

* Automates:

  * Packaging
  * Deployment to Dev/Test/Prod
  * Infrastructure provisioning

---

## 🔹 Jenkins Architecture

* **Master (Controller)**

  * Manages jobs
  * Schedules builds
  * Assigns work to agents
  * Stores configuration

* **Agent (Node/Slave)**

  * Executes build jobs
  * Can be Linux/Windows/Mac
  * Can run inside Docker/Kubernetes

* Communication via:

  * SSH
  * JNLP
  * WebSocket

---

## 🚀 Jenkins Agents – Theory & Key Points to Remember

---

## 1️⃣ What is a Jenkins Agent?

A **Jenkins Agent (formerly called Slave)** is a machine that connects to the Jenkins Controller and executes build jobs.

🔹 Controller = Brain (manages jobs, UI, scheduling)
🔹 Agent = Worker (executes builds, tests, deployments)

👉 Used for **distributed builds**, scalability, and workload separation.

---

## 2️⃣ Why Jenkins Agents are Needed?

✔️ Parallel builds
✔️ Load distribution
✔️ Different OS environments (Linux/Windows/macOS)
✔️ Tool-specific environments (Java, Docker, Node, etc.)
✔️ Isolate heavy workloads
✔️ Secure production deployments

---

## 3️⃣ Jenkins Architecture (Controller + Agents)

```
             +------------------+
             |  Jenkins         |
             |  Controller      |
             +------------------+
                     |
      ---------------------------------
      |               |               |
+-------------+  +-------------+  +-------------+
| Linux Agent |  | Windows     |  | Docker      |
| (Build)     |  | Agent       |  | Agent       |
+-------------+  +-------------+  +-------------+
```

Controller schedules → Agents execute.

---

## 4️⃣ Types of Jenkins Agents

### 🔹 1. Permanent Agent (Static Agent)

* Always running
* Manually configured
* Suitable for stable infrastructure

### 🔹 2. Dynamic Agent

* Created on demand
* Auto-destroyed after job
* Used in cloud/Kubernetes

### 🔹 3. Docker Agent

* Runs job inside container
* Clean environment every build

### 🔹 4. Kubernetes Agent

* Uses Pod as agent
* Very scalable
* Common in DevOps pipelines

---

## 5️⃣ Agent Communication Methods

✔️ SSH (Linux)
✔️ Windows Service
✔️ JNLP (Java Web Start)
✔️ Kubernetes plugin
✔️ Docker plugin

---

## 6️⃣ Important Terminologies

| Term      | Meaning                               |
| --------- | ------------------------------------- |
| Node      | Machine configured in Jenkins         |
| Agent     | Worker node                           |
| Executor  | Number of parallel jobs agent can run |
| Label     | Tag used to target specific agent     |
| Workspace | Directory where build runs            |

---

## 7️⃣ Jenkinsfile Example Using Agent

### Declarative Pipeline

```groovy
pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh 'echo Building...'
            }
        }
    }
}
```

### Specific Agent Label

```groovy
pipeline {
    agent { label 'linux' }
}
```

### Docker Agent

```groovy
pipeline {
    agent {
        docker {
            image 'node:18'
        }
    }
}
```

---

## 8️⃣ Executor Concept (Important for Interview)

* 1 executor = 1 parallel build
* If agent has 4 executors → can run 4 builds simultaneously
* Too many executors = CPU overload

👉 Best Practice:
Executors = Based on CPU cores & workload type

---

## 9️⃣ Best Practices

✔️ Keep Controller lightweight
✔️ Run builds on agents only
✔️ Use labels wisely
✔️ Use dynamic agents in cloud
✔️ Monitor disk space
✔️ Clean workspaces
✔️ Use containerized agents for consistency
✔️ Restrict production access

---

## 🔟 Common Interview Questions

**Q1: Why not run builds on Controller?**
👉 It affects performance & security.

**Q2: What is difference between Node & Agent?**
👉 Node = Configured machine.
👉 Agent = Worker process running on node.

**Q3: How do agents communicate?**
👉 SSH, JNLP, Kubernetes plugin.

**Q4: What is label in Jenkins?**
👉 Used to assign job to specific agent.

---

## 1️⃣1️⃣ Static vs Dynamic Agents (Comparison)

| Feature     | Static Agent  | Dynamic Agent      |
| ----------- | ------------- | ------------------ |
| Setup       | Manual        | Automated          |
| Cost        | Higher        | Optimized          |
| Scalability | Limited       | High               |
| Use Case    | On-prem infra | Cloud-native CI/CD |

---

## 1️⃣2️⃣ Points to Remember (Exam/Interview Quick Notes)

⭐ Jenkins follows Master-Agent architecture
⭐ Agents execute jobs
⭐ Executors control parallelism
⭐ Labels route jobs
⭐ Use Docker/K8s agents for modern pipelines
⭐ Never overload controller
⭐ Workspace cleanup is important
⭐ Agents can run on different OS

---

## 🔹 Jenkins Components

* Job / Project
* Build
* Pipeline
* Plugin
* Workspace
* Executor
* Node
* Trigger

---

## 🔹 Types of Jobs

* Freestyle Project
* Pipeline Project
* Multibranch Pipeline
* Folder
* Maven Project

---

## 🔹 Pipeline Concepts

* Defined as **Code (Pipeline as Code)**
* Stored in `Jenkinsfile`
* Written in **Groovy DSL**

### Pipeline Types:

* Declarative Pipeline (recommended)
* Scripted Pipeline

---

## 🔹 Important Pipeline Blocks

```groovy
pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo "Building..."
      }
    }
  }
}
```

Key Blocks:

* pipeline
* agent
* stages
* stage
* steps
* post
* environment
* parameters

---

## 🔹 Jenkins Triggers

* Poll SCM
* Webhook (GitHub/GitLab)
* Scheduled (CRON)
* Manual Trigger
* Upstream Job

---

## 🔹 Plugins (Very Important)

Common Plugins:

* Git Plugin
* Pipeline Plugin
* Docker Plugin
* Kubernetes Plugin
* Blue Ocean
* SonarQube
* Email Extension

👉 Jenkins strength = Plugin ecosystem

---

## 🔹 Security Concepts

* Matrix-based security
* Role-based access control (RBAC)
* Credentials management
* API Tokens
* Secret Text / Username-Password / SSH Key
* Integration with LDAP / AD / SSO

---

## 🔹 Credentials in Jenkins

Stored securely in:

* Global scope
* Folder scope
* System scope

Used inside pipeline:

```groovy
withCredentials([])
```

---

## 🔹 Jenkins File Structure

* `/var/lib/jenkins` (Linux default home)
* `config.xml`
* `jobs/`
* `workspace/`
* `plugins/`

---

## 🔹 Distributed Builds

* Improves performance
* Scales horizontally
* Used in enterprise CI/CD

---

## 🔹 Backup & Restore

Important to backup:

* JENKINS_HOME
* plugins
* credentials
* jobs configuration

---

## 🔹 High Availability (HA)

Jenkins itself:

* Not fully HA by default
* Use:

  * Load Balancer
  * External DB
  * Cloud agents (K8s)

---

## 🔹 Jenkins vs Other Tools

| Feature          | Jenkins    | GitHub Actions | Azure DevOps |
| ---------------- | ---------- | -------------- | ------------ |
| Open Source      | ✅          | ❌              | ❌            |
| Plugin Ecosystem | Very Large | Limited        | Moderate     |
| On-Prem Support  | Strong     | Limited        | Strong       |
| UI Flexibility   | High       | Medium         | Medium       |

---

## 🔹 Best Practices

* Use Pipeline instead of Freestyle
* Store Jenkinsfile in Git
* Use credentials binding
* Avoid hardcoding secrets
* Use agents instead of master execution
* Regular plugin updates
* Enable backups

---

## 🔹 Common Interview Questions Concepts

* Difference between CI & CD
* Declarative vs Scripted pipeline
* Master vs Agent
* How Jenkins handles parallel stages
* How to secure Jenkins?
* How to scale Jenkins?
* What is Blue Ocean?

---

## 🔹 Advanced Concepts

* Shared Libraries
* Parallel Stages
* Docker agents
* Kubernetes dynamic agents
* Jenkins in Kubernetes
* Infrastructure as Code integration (Terraform, Ansible)

---

```
jenkins | jenkins.pem | SG - Inbound - jenkins-8080 | t3.large, c7i-flex.large

cd Downloads 
chmod 400 jenkins.pem
ssh -i "jenkins.pem" ec2-user@ec2-52-204-224-228.compute-1.amazonaws.com

sudo yum update -y
sudo yum install wget tar tree python -y 

sudo yum install git -y 
git config --global user.name "Atul Kamble"
git config --global user.email "atul_kamble
git config --list 
 
sudo yum install docker -y 
sudo systemctl start docker 
sudo systemctl enable docker 
sudo docker login 
docker --version 

sudo yum install maven -y 
mvn -v

sudo yum install java-21-amazon-corretto.x86_64 -y
java --version 

// copy script from https://www.jenkins.io/doc/book/installing/linux/#red-hat-centos

sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo yum upgrade
# Add required dependencies for the jenkins package
sudo yum install fontconfig java-21-openjdk
sudo yum install jenkins
sudo systemctl daemon-reload

jenkins --version 
sudo systemctl start jenkins 
sudo systemctl enable jenkins
newgrp docker

docker ps
docker run hello-world

sudo usermod -aG docker $USER
sudo usermod -aG docker jenkins
sudo systemctl restart docker
sudo systemctl restart jenkins


http://instance-public-ip:8080

sudo cat /var/lib/jenkins/secrets/initialAdminPassword

// paste password 

Settings >> plugins >> docker, docker pipeline, Blue Ocean, AWS Credentials Plugin

sudo systemctl restart jenkins 

pipeline {
    agent any

    stages {
        stage('dev') {
            steps {
                echo 'I am in dev'
                sh 'python --version'
            }
        }

        stage('staging') {
            steps {
                echo 'I am in stage'
                sh 'docker --version'
            }
        }
        stage('prod') {
            steps {
                echo 'I am in prod'
                sh 'mvn -v'
            }
        }
    }
}
```


# 🚀 Jenkins Setup on EC2 with Git and Docker

This guide helps you set up Jenkins on an EC2 instance with Git and Docker integration.

```
git clone https://github.com/atulkamble/ec2-jenkins.git
cd ec2-jenkins
chmod +x deploy.sh
./deploy.sh
```
# Jenkins using docker
```
// commands after ssh 
sudo yum update -y
sudo yum install docker 
sudo systemctl start docker 
sudo systemctl enable docker 
docker --version 
sudo docker login 
sudo docker images
sudo docker pull jenkins/jenkins:jdk21
sudo docker run -d -p 8080:8080 jenkins/jenkins:jdk21
// browse http://instance-ip:8080
// list containers 
sudo docker container ls        // da6e91230c61
// copy passowrd and paste it 
sudo docker exec -it da6e91230c61 cat /var/jenkins_home/secrets/initialAdminPassword
```
---

## 📌 Prerequisites

* **AWS EC2 Instance:** Amazon Linux 2023 (t3.large recommended)
* **Security Group Ports Open:**

  * SSH: 22
  * HTTP: 80
  * HTTPS: 443
  * Jenkins: 8080
* **Storage:** 30 GB SSD
* **Key Pair:** `jenkins.pem` (ensure secure permissions)

---

## ⚙️ Step 1: Connect to EC2 Instance

```bash
cd Downloads
chmod 400 jenkins.pem
ssh -i "jenkins.pem" ec2-user@<YOUR_EC2_PUBLIC_IP>
```

---

## 📦 Step 2: Install Required Packages

### 1. Update and Install Git

```bash
sudo yum update -y
sudo yum install git -y
git --version
```

### 2. Configure Git (Optional)

```bash
git config --global user.name "Atul Kamble"
git config --global user.email "atul_kamble@hotmail.com"
git config --list
```

### 3. Install Docker

```bash
sudo yum install docker -y
sudo systemctl start docker
sudo systemctl enable docker
```

### 4. Install Java (Amazon Corretto 21)

```bash
sudo dnf install java-21-amazon-corretto -y
or
sudo yum install fontconfig java-21-openjdk
java --version
```

### 5. Install Maven

```bash
sudo yum install maven -y
mvn -v
```

### 6. Install Jenkins

```bash
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo yum upgrade -y
sudo yum install jenkins -y
jenkins --version
```

### 7. Add Jenkins User to Docker Group

```bash
sudo usermod -aG docker jenkins
```

---

## ▶️ Step 3: Start Jenkins

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

---

## 🌐 Step 4: Access Jenkins Web UI

Open your browser and go to:

```
http://<YOUR_EC2_PUBLIC_IP>:8080
```

Unlock Jenkins using the initial admin password:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Paste the password into the Jenkins setup screen and proceed.

---

## ✅ Jenkins is now ready to use!
