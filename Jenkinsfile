pipeline {
    agent any

    stages {
        stage('pre') {
            steps {
                script {
                    env.currentTag = sh(returnStdout: true, script: "git describe --tags --abbrev=0")
                    env.currentTag = env.currentTag.getAt(1..env.currentTag.length() - 1)
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
