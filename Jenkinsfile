pipeline {
    agent any

    stages {
        stage('Checkout Verification') {
            steps {
                echo '===== SOURCE CODE RECEIVED ====='
                sh '''
                    echo "Build Number: ${BUILD_NUMBER}"
                    echo "Workspace: ${WORKSPACE}"
                    echo "Files received from GitHub:"
                    ls -la
                '''
            }
        }

        stage('Validate Application Files') {
            steps {
                echo '===== VALIDATING APPLICATION ====='
                sh '''
                    test -f Dockerfile
                    test -f app/index.html
                    test -f app/style.css

                    echo "All required application files are present."
                '''
            }
        }
stage('Build Docker Image') {
    steps {
        echo '===== BUILDING DOCKER IMAGE ====='
        sh '''
            docker build \
              -t jenkins-automation-lab:${BUILD_NUMBER} .

            echo "Docker image created successfully:"
            docker images jenkins-automation-lab
        '''
    }
} 
    }

        stage('Deploy Application') {
            steps {
                echo '===== DEPLOYING APPLICATION ====='
                sh '''
                    docker rm -f jenkins-lab-web || true

                    docker run -d \
                      --name jenkins-lab-web \
                      --restart unless-stopped \
                      -p 80:80 \
                      jenkins-automation-lab:${BUILD_NUMBER}

                    echo "Application container deployed successfully."
                    docker ps --filter "name=jenkins-lab-web"
                '''
            }
        }

        stage('Health Check') {
            steps {
                echo '===== RUNNING HEALTH CHECK ====='
                sh '''
                    sleep 3
                    curl --fail --silent --show-error http://localhost/ > /dev/null
                    echo "Health check passed. Application is responding."
                '''
            }
        }
}
