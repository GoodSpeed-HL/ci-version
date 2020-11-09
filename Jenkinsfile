pipeline {
    agent any

    stages {
        stage('build'){
            steps {
                sh 'docker build -t helloworld:${env.currentTag} .'
                sh 'docker tag helloworld:${env.currentTag} registry.digitalocean.com/bitcoco/helloworld:${env.currentTag}'
                sh 'docker push registry.digitalocean.com/bitcoco/helloworld:${env.currentTag}'
            }
        }
    }
}
