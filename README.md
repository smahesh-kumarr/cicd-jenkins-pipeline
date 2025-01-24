# Complete End-to-End Maven Project with Jenkins Pipeline

## Overview 🌍

This project demonstrates how to create a Maven-based application with a Jenkins CI/CD pipeline. The pipeline includes stages for **building**, **testing**, and **deploying** to multiple environments (Dev and Prod). It also incorporates **stashing/unstashing artifacts** and deploys to a server using Jenkins.

---

## 🎯 Objectives

1. **Set Up Jenkins**:
   - Master-Agent architecture.
   - Install necessary plugins and tools.
2. **Connect to a Git Repository**:
   - Enable Git Webhook with an access token.
3. **Pipeline Workflow**:
   - **Stages**: Build -> Test -> Deploy (Multistage: Dev/Prod).
   - Stash and unstash artifacts.
4. **Deployment**:
   - Deploy source artifacts to an Ocean World production server.
5. **UI Enhancements**:
   - Add a visually appealing and colorful pipeline view.

---

## 🛠 Prerequisites

### Tools & Packages:
- **Jenkins**:
  - Installed on the Master server.
  - Agent nodes configured for distributed builds.
- **Git**:
  - Ensure Git is installed on Jenkins servers.
- **Java**:
  - Required for Maven.
- **Maven**:
  - Install Maven on Jenkins servers.

### Plugins:
- **Pipeline**
- **Git Plugin**
- **Maven Integration**
- **Blue Ocean**
- **GitHub Integration**

---

## 🌟 Project Setup

### 1. Create a Maven Project Repository 🗂️
- Clone or create a new GitHub repository.
- Add your Maven project structure:
  ```plaintext
  /src/main/java
  /src/test/java
  pom.xml
  Jenkinsfile
  ```

### 2. Add Jenkinsfile 🛠️
Here's the Jenkinsfile to define the CI/CD pipeline:

```groovy
pipeline {
    agent none

    parameters {
        choice(choices: ['Dev', 'Prod'], name: 'select_environment')
    }

    tools {
        maven 'Maven_Tool'
    }

    stages {
        stage('Build') {
            agent { label 'master' }
            steps {
                echo "🔨 Building the project"
                sh 'mvn clean package -DskipTests=true'
            }
            post {
                success {
                    stash includes: '**/target/*.war', name: 'build-artifact'
                }
            }
        }

        stage('Test') {
            agent { label 'master' }
            steps {
                echo "🧪 Running Tests"
                sh 'mvn test'
            }
        }

        stage('Deploy to Dev') {
            when { expression { params.select_environment == 'Dev' } }
            agent { label 'dev-node' }
            steps {
                echo "🚀 Deploying to Dev Environment"
                unstash 'build-artifact'
                sh 'mv target/*.war /var/www/dev'
            }
        }

        stage('Deploy to Prod') {
            when { expression { params.select_environment == 'Prod' } }
            agent { label 'prod-node' }
            steps {
                input message: 'Approve deployment to Prod?'
                echo "🚀 Deploying to Prod Environment"
                unstash 'build-artifact'
                sh 'mv target/*.war /var/www/prod'
            }
        }
    }
}
```

---

### 3. Configure Git Webhook 🔗
- Navigate to your GitHub repository.
- Go to **Settings** -> **Webhooks** -> Add webhook:
  - Payload URL: `http://<JENKINS_URL>:8080/github-webhook/`
  - Content type: `application/json`.
  - Add your **Personal Access Token** with appropriate permissions.

---

## 🌈 UI Enhancements with Blue Ocean
- Use **Blue Ocean** for a modern, colorful pipeline visualization.
- Navigate to `http://<JENKINS_URL>:8080/blue`.
- View the stages with a visually appealing layout.

---

## 📝 Pipeline Workflow

### Build 🛠️:
- Cleans and packages the Maven project.
- Skips tests for faster builds.

### Test 🧪:
- Executes all unit tests.

### Deploy to Dev 🚀:
- Deploys artifacts to the development server.

### Deploy to Prod 🚀:
- Requires manual approval before deploying to the production server.

---

## 🌊 Ocean World Deployment

1. Use the `stash` and `unstash` directives to manage artifacts.
2. Deploy the `.war` file to the production server at `/var/www/prod`.
3. Add colorful console logs for better debugging:
   ```groovy
   echo "🌟 Build Success!"
   echo "🎉 Deployment Complete!"
   ```

---

## 🎨 Final Touch: Emojis and Colors

- Use `echo` with emojis and ANSI colors for better readability:
   ```groovy
   echo "\u001B[32m✔ Build completed successfully!"
   echo "\u001B[31m✖ Test failed!"
   ```

---

## 💻 Running the Pipeline

1. Access Jenkins at `http://<JENKINS_URL>:8080`.
2. Create a **Multibranch Pipeline** job.
3. Point the job to your GitHub repository.
4. Trigger the build manually or via Git Webhook.

---

**Happy CI/CD 🚀!**
