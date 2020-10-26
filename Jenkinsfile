
allImages = [
    "webclient",
    "api",
    "dicom-receiver",
    "fixture-service",
    "tests",
    "test-reference-image-provider",
]

pipeline {
    agent {
        // label "docker"   
        docker{
            image: 'maven:3-alpine'
        }
    }
    stages {
        stage('Config'){
            steps{
                echo "Branch: ${env.BRANCH_NAME}"
            }
        }
        stage('Build') {
            steps {
                script {
                    parallel getBuildStages(allImages)
                }
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


def getBuildStages(images) {
    def stages = [failFast: true]
    allImages.each { image ->
        stages["${image}"] = {
            stage("Building ${image}") {
                script {
                    echo "Hello ${image}"
                }
            }
        }
    }

    return stages
}