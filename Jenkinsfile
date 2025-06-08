pipeline {
    agent any
    environment {
        DOCKERHUB_REPO = 'hortensehouendji/jenkins-static-webapp'
        GITHUB_URL = 'https://github.com/hortensesigue/jenkins-static-webapp.git'
        DOCKERHUB_CREDS = credentials('MyDockerCreds-id')
    }

    stages {
        stage('Source') {
            steps {
                echo 'Checking out the code from Github'
                git branch: 'main', credentialsId: '4a06acf4-d65b-4f9c-9ac8-53dc78cfce66', url: 'https://github.com/hortensesigue/jenkins-static-webapp.git'
            }
        }
        stage('Build') {
            steps {
                echo 'Build Our Docker image'
                // listing files on local server
                // sh 'ls -l'
                // sh 'whoami'
                // sh 'docker build -t hortensehouendji/jenkins-static-webapp:v1 .'
                sh 'docker build -t ${DOCKERHUB_REPO}:v${BUILD_NUMBER} .'
                echo 'list docker image'
                sh 'docker images'
            }
        }
        stage('Login to Dockerhub') {
            steps{
            echo 'login into dockerhub'
            sh 'docker login -u${DOCKERHUB_CREDS_USR} -p${DOCKERHUB_CREDS_PSW}'
            sh 'echo dockerhub login success'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy the image to DockerHub'
                sh 'docker login'
                sh 'docker push ${DOCKERHUB_REPO}:v${BUILD_NUMBER}'
                echo 'done et done and yes yup yup yup'
            }
        }
    }
}

