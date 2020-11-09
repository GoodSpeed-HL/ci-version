pipeline {
    agent any

    stages {
        stage('pre') {
            steps {
                git "https://github.com/GoodSpeed-HL/ci-version.git"
                
                script {
                    env.currentTag = sh(returnStdout: true, script: "git describe --tags --abbrev=0").trim()
                }
                echo "${currentTag}"
            }
        }
        stage('build'){
            steps {
                sh 'docker build -t helloworld:${env.currentTag} .'
                sh 'docker tag helloworld:${env.currentTag} registry.digitalocean.com/bitcoco/helloworld:${env.currentTag}'
                sh 'docker push registry.digitalocean.com/bitcoco/helloworld:${env.currentTag}'
            }
        }
    }
}
