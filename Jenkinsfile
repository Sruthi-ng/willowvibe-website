pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the Docker image...'
                script {
                    // Build the image and tag it with the name 'willowvibe-website'
                    docker.build('willowvibe-website', '.')
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the website...'
                script {
                    // Stop and remove any old container with the same name
                    // '-f' means force, so it won't fail if the container doesn't exist
                    sh 'docker stop willowvibe-container || true'
                    sh 'docker rm willowvibe-container || true'

                    // Run the new image as a container
                    // -d runs it in the background
                    // -p 80:80 maps your PC's port 80 to the container's port 80
                    // --name gives the running container a memorable name
                    sh 'docker run -d -p 80:80 --name willowvibe-container willowvibe-website'
                }
            }
        }
    }
}