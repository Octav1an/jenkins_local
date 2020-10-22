pipeline {
    agent {
        node{
            label "docker"   
        }
    }

    stages {
        stage('Config'){
            steps{
                echo "Branch: ${env.BRANCH_NAME}"
                sh "docker image ls"
                sh "docker volume ls"
                sh "docker network ls"
                sh "docker container ls"
                sh "df -h"
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
