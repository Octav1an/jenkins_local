
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
        label "docker"   
    }
    environment {
        GLOBAL_MSG = 'hi there'
    }
    stages {
        stage('Config'){
            steps{
                echo "Branch: ${env.BRANCH_NAME}"
            }
        }
        stage('Build') {
            parallel {
                stage('Test parallel'){
                    steps{
                        echo "parallel here"
                    }
                }
                stage ('other') {
                    steps {
                        script {
                            parallel getBuildStages(allImages)
                        }
                    }
                }
            }

        }
        stage('Test') {
            steps {
                echo 'Testing..'
                echo "${GLOBAL_MSG}"
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