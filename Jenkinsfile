pipeline {
    agent any

    environment{
        
        registry = "vfedorch/prikm"
        registryCredential = 'dockerhub_token'        
    }

    stages {
        stage('Start') {
            steps {
                echo 'Lab_2: started by GitHub'
            }
        }

        stage('Image build') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                    }
            }
        }

        stage('Push to registry') {
            steps {
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }

        stage('Cleaning Up') {
                steps{
                  sh "docker rmi --force $registry:$BUILD_NUMBER"
                }
            }

        // stage('Deploy image'){
        //     steps{
        //         sh "docker run -d -p 80:80 nginx/custom:latest"
        //     }
        // }
    }
}
