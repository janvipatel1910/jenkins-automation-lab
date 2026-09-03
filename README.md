# Jenkins CI/CD Automation Lab

A hands-on DevOps project demonstrating an automated CI/CD pipeline using Jenkins, Docker, GitHub, Linux, and AWS EC2.

The application source code is stored in GitHub. Jenkins monitors the repository for changes, executes a multi-stage pipeline, builds a Docker image, deploys the container to an AWS EC2 instance, and performs an automated health check to verify that the application is available.

## Architecture

Developer
   ↓
GitHub Repository
   ↓
Jenkins CI/CD Pipeline
   ↓
Docker Image Build
   ↓
Docker Container
   ↓
AWS EC2
   ↓
Live Web Application

## Technologies Used

- AWS EC2
- Jenkins
- Docker
- Git & GitHub
- Linux
- Nginx
- HTML/CSS
## CI/CD Pipeline

The Jenkins pipeline is defined as code in the `Jenkinsfile` and contains five automated stages:

1. **Checkout Verification**  
   Confirms that Jenkins has received the latest source code from GitHub and displays the build and workspace information.

2. **Validate Application Files**  
   Verifies that the Dockerfile and required application files exist before continuing the pipeline.

3. **Build Docker Image**  
   Builds a versioned Docker image using the Jenkins build number.

4. **Deploy Application**  
   Removes the previous application container and deploys the newly built version on the EC2 instance.

5. **Health Check**  
   Sends an HTTP request to the deployed application and fails the pipeline if the application is not responding successfully.

## Automated Deployment Workflow

Jenkins uses SCM polling to monitor the `main` branch for new commits.

When a new change is pushed:

`Code Change → Git Push → GitHub → Jenkins → Docker Build → Deployment → Health Check`

This workflow was tested by updating the application, pushing the change to GitHub, and allowing Jenkins to automatically trigger a new build and deploy the updated version without manually selecting **Build Now**.
