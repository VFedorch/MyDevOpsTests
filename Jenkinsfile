pipeline {
    agent any

    stages {
        stage('Start') {
            steps {
                echo 'Lab_2: started by GitHub'
            }
        }

        stage('Image build') {
            steps {
                sh "docker build -t vfedorch/prikm:latest ."
                sh "docker tag nginxtest vfedorch/prikm:latest"
                sh "docker tag nginxtest vfedorch/prikm:$BUILD_NUMBER"
            }
        }

        stage('Push to registry') {
            steps {
                withDockerRegistry([ credentialsId: "dockerhub_token", url: "" ]) {
                    sh  "docker push vfedorch/prikm:latest"
                    sh  "docker push vfedorch/prikm:$BUILD_NUMBER"
                }
            }
        }

        // stage('Cleaning Up') {
        //         steps{
        //           sh "docker rmi --force vfedorch/prikm:$BUILD_NUMBER"
        //         }
        //     }

        stage('Deploy image'){
            steps{
                sh "docker run -d -p 80:80 vfedorch/prikm"
            }
        }
    }
}
