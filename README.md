# TandinYoezerWangmo_02250374_DSO101_A1
https://github.com/yoezer33/TandinYoezerWangmo_02250374_DSO101_A1.git

# Todo App- fullstack with CI/CDpipeline
## My information
- **Name:** Tandin Yoezer Wangmo
- **Student ID:** 02250374
---
## Assignment 3 - CI/CD Pipeline

### Pipeline Overview
This project uses a Continuous Integration and Continuous Deployment (CI/CD) pipeline to automate the build and deployment process. Whenever code is pushed to the main branch, the pipeline runs automatically and performs the following steps:

a. Builds Docker images for both the backend and frontend applications
b. Pushes the built images to DockerHub for storage
c. Triggers a redeployment on Render.com to update the live application

This automation helps ensure that the latest version of the project is always deployed without manual intervention.

### Tools Used
- **Docker** - used to containerize both the frontend and backend applications. This ensures that the app runs consistently across different environments.
- **GitHub Actions** - GitHub Actions is used to automate the CI/CD workflow. It handles building, testing, and deploying the application whenever changes are pushed.
- **DockerHub** - DockerHub acts as a container registry where the built Docker images are stored and managed.
- **Render.com** - Render is used to host and deploy the backend service. It automatically updates the application when triggered by the pipeline.

### Live Deployment
- **Backend:** https://be-todo-backend.onrender.com
- **Backend API test:** https://be-todo-backend.onrender.com/tasks

### GitHub Secrets Used
- DOCKERHUB_USERNAME
- DOCKERHUB_TOKEN
- RENDER_DEPLOY_HOOK_URL

### Challenges Faced
During the implementation of the CI/CD pipeline, a few issues were encountered:

- The frontend Docker build initially failed due to a permission denied error with react-scripts
- This issue was resolved by modifying file permissions using chmod and directly referencing the react-scripts path
- The Render deployment step also failed at first because the deploy hook URL was missing, which caused a curl error
- After adding the correct deploy hook URL, the deployment worked successfully

### Learning Outcomes
Through this assignment, the following key skills were developed:

- Understanding how to containerize applications using Docker
- Learning how to automate workflows using GitHub Actions
- Gaining experience with deploying applications using Render.com
- Understanding how to securely manage sensitive data using GitHub    Secrets

## Screnshots
- img1 =GitHub Action greenruns
- img2 =render service live
- img3 =GitHub Secrets
- img5 =docker img
