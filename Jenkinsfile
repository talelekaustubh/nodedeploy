// pipeline {
//     agent any

//     environment {
//         DOCKER_CREDENTIALS_ID = 'docker-hub-credentials'  // Docker Hub credentials stored in Jenkins
//         DOCKER_IMAGE = 'sksupremeboss/nodeapp'                          // Name of the Docker image
//         DOCKER_TAG = 'latest'                             // Tag for the Docker image
//         DOCKER_REGISTRY = 'docker.io/sksupremeboss' // Docker Hub username
//     }

//     stages {
//         stage('Build Docker Image') {
//             steps {
//                 script {
//                     // Build the Docker image from the Dockerfile in the root directory
//                     docker.build("${DOCKER_REGISTRY}/${DOCKER_IMAGE}:${DOCKER_TAG}")
//                 }
//             }
//         }

//         stage('Push Docker Image to Registry') {
//             steps {
//                 script {
//                     // Log in to Docker Hub and push the image
//                     docker.withRegistry('https://docker.io', "${DOCKER_CREDENTIALS_ID}") {
//                         docker.image("${DOCKER_REGISTRY}/${DOCKER_IMAGE}:${DOCKER_TAG}").push()
//                     }
//                 }
//             }
//         }
//     }
// }

pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'docker-hub-credentials' // Docker Hub credentials stored in Jenkins
        DOCKER_IMAGE = 'nodeapp'                         // Name of the Docker image
        DOCKER_TAG = 'latest'                            // Tag for the Docker image
        DOCKER_REGISTRY = 'docker.io'                     // Docker Hub registry URL
        REPO_NAME = 'sksupremeboss/nodeapp'               // Docker Hub repository name
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image and tag it
                    def customImage = docker.build("${REPO_NAME}:${DOCKER_TAG}")
                }
            }
        }

        stage('Push Docker Image to Registry') {
            steps {
                script {
                    // Log in to Docker Hub and push the image
                    docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_CREDENTIALS_ID}") {
                        docker.image("${REPO_NAME}:${DOCKER_TAG}").push()
                    }
                }
            }
        }
    }
}
