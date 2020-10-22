
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
        node{
            label "docker"   
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
                    sh "Hello ${image}"
                }
            }
        }
    }

    return stages
}