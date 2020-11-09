def currentTag
pipeline {
    agent { dockerfile true }
    stages {
        stage('Test') {
            steps {
                currentTag = sh(returnStdout: true, script: "git describe --tags --abbrev=0")
               echo "${currentTag}"
            }
        }
    }
}