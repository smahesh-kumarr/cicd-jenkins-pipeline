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
