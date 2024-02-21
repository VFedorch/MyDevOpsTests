pipeline {
    agent { dockerfile true }

    stages {
        stage('Build Nginx:custom docker image') {
            steps {
                echo 'Lab_1: Hello World'
            }
        }
    }
}
node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("nginx/custom")
    }

    stage('Test image') {
        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_creds') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
