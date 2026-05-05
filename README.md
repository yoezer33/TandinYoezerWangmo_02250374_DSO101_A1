# TandinYoezerWangmo_02250374_DSO101_A1
https://github.com/yoezer33/TandinYoezerWangmo_02250374_DSO101_A1.git

# Todo App- fullstack with CI/CDpipeline
## My information
- **Name:** Tandin Yoezer Wangmo
- **Student ID:** 02250374
---
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
