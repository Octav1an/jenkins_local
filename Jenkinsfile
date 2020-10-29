
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
                    stash includes: "webclient/build/**", name: "webclient-build"
                    bat "dir"
                }
            }

        }
        stage('Test') {
            steps {
                echo 'Testing..'
                echo "${GLOBAL_MSG}"
                dir("${WORKSPACE}\unstashed")
                script{
                    
                    bat "dir"
                    unstash name: "webclient-build"
                    bat "dir"
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}


// def getBuildStages(images) {
//     def stages = [failFast: true]
//     allImages.each { image ->
//         stages["${image}"] = {
//             stage("Building ${image}") {
//                 script {
//                     echo "Hello ${image}"
//                 }
//             }
//         }
//     }

//     return stages
// }