pipeline {
    agent {
        docker {
            image 'docker:latest'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the Docker image...'
                script {
                    // Use the plugin's built-in build command, which solves the path issue
                    docker.build('willowvibe-website', '.')
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the website...'
                // We can keep using 'sh' for these simple commands
                sh 'docker stop willowvibe-container || true'
                sh 'docker rm willowvibe-container || true'
                sh 'docker run -d -p 80:80 --name willowvibe-container willowvibe-website'
            }
        }
    }
}