pipeline {
    agent any

    stages {
        stage('pre') {
            steps {
                script {
                    env.currentTag = sh(returnStdout: true, script: "git describe --tags --abbrev=0").trim()
                }
                echo "${currentTag}"
            }
        }
        stage('build'){
            steps {
                sh 'docker build -t helloworld:${currentTag} .'
                sh 'docker tag helloworld:${currentTag} registry.digitalocean.com/bitcoco/helloworld:${currentTag}'
                sh 'docker push registry.digitalocean.com/bitcoco/helloworld:${currentTag}'
            }
        }
    }
}
