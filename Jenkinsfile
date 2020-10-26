
allImages = [
    "api",
    "dicom-receiver",
    "fixture-service",
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
            steps{
                script{
                    parallel getBuildStages(allImages)
                }
            }
            parallel {
                stage('webclient'){
                    steps{
                        echo "webclient here"
                    }
                }
                stage() {
                    steps{
                        echo "tests here"
                    }
                }
                // stage('OTHER'){

                // }
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