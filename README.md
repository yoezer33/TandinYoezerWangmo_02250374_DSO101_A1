# TandinYoezerWangmo_02250374_DSO101_A1
https://github.com/yoezer33/TandinYoezerWangmo_02250374_DSO101_A1.git

# Todo App- fullstack with CI/CDpipeline
## My information
- **Name:** Tandin Yoezer Wangmo
- **Student ID:** 02250374
---

# DSO101 Assignment 2 - CI/CD Pipeline with Jenkins
**Student:** Tandin Yoezer Wangmo  
**Student ID:** 02250374  
**Course:** DSO101 - Continuous Integration and Continuous Deployment  

---

## Overview
This assignment shows how  the setup of a Jenkins CI/CD pipeline to automate the build, test, and deployment of a Todo List React application developed in Assignment 1.

---

## Tools & Technologies
| Tool | Purpose |
|------|---------|
| Jenkins | CI/CD automation |
| GitHub | Source code hosting |
| Node.js 26.1.0 | JavaScript runtime |
| Jest | Unit testing framework |
| jest-junit | JUnit test reports for Jenkins |
| React | Frontend framework |
| npm | Package management |

---

## Pipeline Stages
The Jenkins pipeline have of the 3 stages:

### 1. Checkout
Pulls the latest source code from the GitHub repository:https://github.com/yoezer33/TandinYoezerWangmo_02250374_DSO101_A1
### 2. Install
Installs all required Node.js dependencies using:
```bash
npm install
```

### 3. Test
Runs unit tests using Jest with JUnit reporting:
```bash
npm test
```

---

## Pipeline Configuration

### Jenkinsfile
```groovy
pipeline {
    agent any
    tools {
        nodejs 'NodeJS'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/yoezer33/TandinYoezerWangmo_02250374_DSO101_A1.git'
            }
        }
        stage('Install') {
            steps {
                bat 'npm install'
            }
        }
        stage('Test') {
            steps {
                bat 'npm test'
            }
        }
    }
}
```

### package.json Test Configuration
```json
"scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build",
    "test": "jest --ci --reporters=default --reporters=jest-junit"
},
"devDependencies": {
    "jest": "^27.5.1",
    "jest-junit": "^17.0.0"
}
```

---

## Setup Instructions

### 1. Jenkins Setup
- Download and install Jenkins from [jenkins.io](https://jenkins.io/download)
- Run Jenkins on `localhost:8080`
- Install required plugins:
  - NodeJS Plugin
  - Pipeline
  - GitHub Integration
  - Git

### 2. Configure Node.js in Jenkins
- Go to **Manage Jenkins → Tools → NodeJS**
- Add NodeJS installation with version 26.1.0
- Name it `NodeJS`

### 3. Add GitHub Credentials
- Go to **Manage Jenkins → Credentials**
- Add **Username with Password**
- Use GitHub Personal Access Token (PAT) as password

### 4. Create Pipeline Job
- Click **New Item → Pipeline**
- Set Definition to **Pipeline script from SCM**
- Set SCM to **Git**
- Enter repository URL
- Set branch to `*/main`
- Set Script Path to `Jenkinsfile`

---

## Test Results
The pipeline runs a simple unit test using Jest:

```javascript
test('simple test', () => {
  expect(1 + 1).toBe(2);
});
```

---

## Challenges Faced

### 1. Jenkins Login Issue
- Could not sign in with the original credentials
- **Solution:** Disabled security in `config.xml` located at `C:\ProgramData\Jenkins\.jenkins\config.xml`, reset the password, then re-enabled security

### 2. Docker Container Conflict
- A previous Jenkins Docker container was conflicting with the Jenkins Windows service
- **Solution:** Stopped and removed the Jenkins Docker containers using `docker stop` and `docker rm` commands

### 3. Plugin Installation Issues
- Jenkins plugin update center was redirecting to a Chinese mirror that was inaccessible
- **Solution:** Manually downloaded `.hpi` plugin files and uploaded them via Jenkins Advanced Settings

### 4. Missing Test Script
- The `package.json` did not have a test script configured
- **Solution:** Added Jest and jest-junit as dev dependencies and configured the test script

### 5. Git Push Failures
- Large `node_modules` folder caused HTTP 408 timeout errors during push
- **Solution:** Created `.gitignore` file to exclude `node_modules` and removed it from git tracking using `git rm -r --cached node_modules`

### 6. Wrong Repository URL
- Jenkins was pulling from the wrong GitHub repository
- **Solution:** Updated both the Jenkins pipeline configuration and the Jenkinsfile to use the correct repository URL

---

## GitHub Repository
[https://github.com/yoezer33/TandinYoezerWangmo_02250374_DSO101_A1](https://github.com/yoezer33/TandinYoezerWangmo_02250374_DSO101_A1)


## Assignment 3 - CI/CD Pipeline

### Pipeline Overview
In this project, I used a CI/CD pipeline to make the process of building and deploying the application automatic. This means I don’t have to manually update or run everything each time I make changes.
Whenever I push new code to the main branch, the pipeline starts running by itself and completes a series of steps:
- Building Docker images
First, the pipeline creates Docker images for both the backend and frontend.These images are  like packaged versions of the app that include everything needed to run them properly.
- Uploading images to DockerHub
After building the images, the pipeline sends (pushes) them to DockerHub. This works like an online storage space where these app packages are saved and can be accessed anytime.
- Triggering deployment on Render.com
Finally, the pipeline sends a signal to Render.com to redeploy the application. This updates the live version of the app with the newest changes.
Because of this automation, the latest version of the project is always updated online without needing to do the steps manually. It saves time, reduces mistakes, and makes the whole process smoother.

### Tools Used
- **Docker** - used to containerize both the frontend and backend applications. This ensures that the app runs consistently across different environments.
- **GitHub Actions** - GitHub Actions is used to automate the CI/CD workflow. It handles building, testing, and deploying the application whenever changes are pushed.
- **DockerHub** - DockerHub acts as a container registry where the built Docker images are stored and managed.
- **Render.com** - Render is used to host and deploy the backend service. It automatically updates the application when triggered by the pipeline.

### Live Deployment
- **Backend:** https://be-todo-backend.onrender.com
- **Backend API test:** https://be-todo-backend.onrender.com/tasks

### GitHub Secrets Used
In this assigments, I used GitHub Secrets to safely store important information that should not be shared publicly. These secrets act like hidden keys that allow the system to work securely.

- DOCKERHUB_USERNAME
This is the username of my DockerHub account. It helps the system know which account to use when uploading Docker images.
- DOCKERHUB_TOKEN
This is a special password (access token) used instead of my real password. It allows GitHub Actions to log in to DockerHub securely and push images without exposing my actual credentials.
- RENDER_DEPLOY_HOOK_URL
This is a special link provided by Render.com. When the pipeline sends a request to this link, it tells Render to automatically redeploy the application with the latest updates.

### Challenges Faced
While setting up the CI/CD pipeline, I faced a few problems, but solving them helped me understand the process better:

- Frontend Docker build error
At first, the frontend Docker build did not work because of a permission denied error related to react-scripts. This means the system was not allowed to run that file.
- Fixing the permission issue
To solve this, I changed the file permissions using chmod, which gave the system the required access. I also directly used the correct path to react-scripts to make sure it could run properly inside the container.
- Render deployment error
Another issue happened during deployment. The pipeline tried to trigger Render, but it failed because the deploy hook URL was missing. This caused a curl error since there was no valid link to send the request to.
- Final fix for deployment
After adding the correct deploy hook URL in GitHub Secrets, the pipeline was able to successfully notify Render, and the application deployed without any issues.

### Learning Outcomes
- Using Docker to package applications
I learned how to use Docker to put my application into a “container.” Container is like a box that holds everything the app needs to run. This makes sure the app works the same way on any computer, without breaking.
- Automating tasks with GitHub Actions
I learned how to make GitHub do work automatically. For example, whenever I upload new code, GitHub Actions can build and prepare my app without me doing it manually.
- Deploying applications using Render.com
I learned how to put my application on the internet so other people can use it. Render.com helps take my app and run it online, so it becomes a real working website or API.
- Keeping important information safe with GitHub Secrets
I learned how to store sensitive information like passwords and tokens safely. Instead of writing them directly in my code (which is risky), I used GitHub Secrets to hide them, like keeping my mom's gold in a safe locker

## Screnshots
- img1 =GitHub Action greenruns
- img2 =render service live
- img3 =GitHub Secrets
- img5 =docker img
