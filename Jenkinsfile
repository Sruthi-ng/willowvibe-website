pipeline {
    // Define a Docker container to be our agent
    agent {
        docker {
            image 'docker:latest'
            // This makes the host's Docker socket available inside this agent container
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the Docker image...'
                // This 'sh' step will now run inside the 'docker:latest' container
                sh 'docker build -t willowvibe-website .'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the website...'
                script {
                    // Stop and remove any old container with the same name
                    sh 'docker stop willowvibe-container || true'
                    sh 'docker rm willowvibe-container || true'

                    // Run the new image as a container
                    sh 'docker run -d -p 80:80 --name willowvibe-container willowvibe-website'
                }
            }
        }
    }
}