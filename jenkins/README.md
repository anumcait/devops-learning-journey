# Jenkins Overview

## Overview of Continuous Integration

Continuous Integration (CI) is a software development practice where developers merge their code changes frequently into a shared repository. Each integration is verified by an automated build and testing process to detect issues early.

### Benefits of CI:

- Early detection of bugs
- Faster development cycles
- Improved collaboration
- Reduced integration problems



## Difference Between Continuous vs Traditional Integration

| Aspect               | Traditional Integration                | Continuous Integration                |
| -------------------- | -------------------------------------- | ------------------------------------- |
| Code Integration     | Done at the end of a development cycle | Done frequently (daily or per commit) |
| Bug Detection        | Late in the cycle                      | Early in development                  |
| Automation           | Manual builds and tests                | Automated builds and tests            |
| Deployment Frequency | Infrequent                             | Frequent                              |
| Feedback Loop        | Slow                                   | Fast                                  |

## Overview of Jenkins

Jenkins is an open-source automation server used to implement CI/CD workflows. It helps in automating software build, test, and deployment processes.



### Features of Jenkins:

- Easy setup and extensibility
- Supports multiple plugins
- Scalable through Master-Slave architecture
- Integration with various tools

## Jenkins Master-Slave Architecture

Jenkins supports a distributed build system using the master-slave architecture.



### Components:

- **Jenkins Master:** Controls the build process and distributes tasks.
- **Jenkins Slave:** Executes build jobs assigned by the master.

### Advantages:

- Load balancing for large projects
- Parallel execution of jobs

## Jenkins Installation and Configuration

### Steps to Install Jenkins:

1. Download Jenkins from [Jenkins Official Website](https://www.jenkins.io/)
2. Install Java (Jenkins requires Java to run)
3. Run Jenkins using `java -jar jenkins.war`
4. Access Jenkins through `http://localhost:8080`
5. Complete the initial setup and install recommended plugins



## Jenkins Plugins

Jenkins provides numerous plugins to enhance its functionality.

### Popular Plugins:

- **Git Plugin** – Enables Git integration
- **Pipeline Plugin** – Facilitates CI/CD pipelines
- **Email Extension Plugin** – Enables email notifications

## Jenkins Management

Jenkins allows administrators to manage users, configure security settings, and monitor builds.

### Key Management Features:

- User authentication and authorization
- Backup and restore
- System logs monitoring

## Jenkins Freestyle and Pipeline Jobs

- **Freestyle Jobs:** Basic jobs that define build steps sequentially.
- **Pipeline Jobs:** Advanced jobs defined in code with greater flexibility.

## Scripted and Declarative Pipelines

### **Scripted Pipeline** (Groovy-based)

```groovy
node {
    stage('Build') {
        echo 'Building...'
    }
    stage('Test') {
        echo 'Testing...'
    }
    stage('Deploy') {
        echo 'Deploying...'
    }
}
```

### **Declarative Pipeline** (Simpler syntax)

```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying...'
            }
        }
    }
}
```

## Configuring Slave Node to Jenkins

### Steps to Add a Slave Node:

1. Go to **Manage Jenkins > Manage Nodes and Clouds**
2. Click **New Node** and provide a name
3. Choose **Permanent Agent** and configure workspace
4. Set up SSH for connection
5. Save and launch the agent



## Configure Tomcat Server

### Steps to Configure Tomcat:

1. Download Apache Tomcat from [Tomcat Official Site](https://tomcat.apache.org/)
2. Extract the files and configure `server.xml`
3. Deploy applications by placing WAR files in the `webapps` directory

## Integrate and Deploy to Tomcat Server Using Jenkins

1. Install the **Deploy to Container Plugin**
2. Configure the Tomcat server details in **Jenkins Global Tool Configuration**
3. Define a pipeline to build and deploy

### Example Deployment Pipeline:

```groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'tomcat-cred', path: '', url: 'http://localhost:8080')],
                war: 'target/myapp.war'
            }
        }
    }
}
```

## Jenkins Build Triggers

### Available Build Triggers:

- **SCM Polling:** Triggers when code changes in repositories
- **Webhook:** GitHub/GitLab webhooks to trigger builds
- **Scheduled Builds:** Run builds at specific intervals

## Enable Email Notifications

### Steps to Configure Email Notifications:

1. Install the **Email Extension Plugin**
2. Configure SMTP settings in **Manage Jenkins > Configure System**
3. Use the following pipeline step to send emails:

```groovy
emailext subject: 'Build Status', 
    body: 'Build ${BUILD_NUMBER} finished.', 
    to: 'team@example.com'
```



---

# Jenkins Interview Questions with Answers

### Real-Time Scenario-Based Questions:

1. **Your Jenkins build is failing after a recent commit. How would you troubleshoot it?**

   - Check the Jenkins console output.
   - Review the commit changes and possible syntax errors.
   - Verify dependency issues and environment configurations.

2. **How would you set up Jenkins to deploy a microservices-based application?**

   - Use a **Multi-Branch Pipeline**.
   - Configure **Docker and Kubernetes plugins**.
   - Automate **CI/CD pipeline** for each microservice.

3. **Your Jenkins job is running very slowly. What steps would you take to optimize it?**

   - Enable **parallel execution**.
   - Use **distributed builds with slave nodes**.
   - Cache dependencies to avoid redundant downloads.

4. **How would you rollback a deployment using Jenkins?**

   - Use Jenkins **Build History** to redeploy the last successful build.
   - Implement a **versioning strategy**.
   - Use a rollback script in your pipeline.

These updates now include images for better understanding. Let me know if you need more refinements! 🚀

## How to setup for Shared Library

- Configure Jenkins Global Pipeline Library
Go to Jenkins UI:

- Navigate to Manage Jenkins > Configure System.
Add the Shared Library:

- Scroll down to the Global Pipeline Libraries section.
Click Add to add a new library.
- Configure the Library:

Name: Enter the name of your library (e.g., my-jenkins-library).
Source Code Management: Select Git.
Repository URL: Enter the URL of your Git repository, like https://github.com/anumcait/devops-learning-journey.git.
Credentials: If the repository is private, select or add credentials (e.g., GitHub personal access token or SSH key).
Branch: Set the branch name (e.g., main).

**Note **
If any one create a sub folder for jenkins library (like me), you will get error while building.

I googled and found solution. Below is the solution

![image](https://github.com/user-attachments/assets/c577b1a2-933c-47f4-bd9e-53f7c55e230c)
![image](https://github.com/user-attachments/assets/e3d71188-8507-4be7-af26-740d436c7795)

- Mention sub folder in the Library path at the bottom of the Global Trusted Pipeline Libraries. (default ./ will be existed, change to ./<<your_custom_folder>>
- Ex: ./jenkins

Finally your folder structure look like this:
devops-learning-journey/
├── jenkins/
│   └── vars/
│       └── myVar.groovy  <-- Your Groovy file here
