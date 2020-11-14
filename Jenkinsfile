pipeline {
    agent any

    stages {
        stage('pre') {
            steps {
                script {
                    env.currentTag = sh(returnStdout: true, script: "git describe --tags --abbrev=0")
                    env.currentTag = env.currentTag.getAt(1..env.currentTag.length() - 1)
                    sh 'cat package.json'
                    env.service =  sh(returnStdout: true, script: "cat package.json | grep service | head -1 | awk -F: '{ print \$2 }' | sed 's/[\",]//g' | tr -d '[[:space:]]'")
                }
                echo "${currentTag}"
                echo "${service}"
            }
        }
        stage('build'){
            steps {
                sh 'docker build -t ${service}:${currentTag} .'
                sh 'docker tag ${service}:${currentTag} registry.digitalocean.com/bitcoco/${service}:${currentTag}'
                sh 'docker push registry.digitalocean.com/bitcoco/${service}:${currentTag}'
            }
        }

        stage('post'){
            steps {
                script {
                    sh 'curl https://pipelines.bitcoco.ca/job/short-test/buildWithParameters --user bot:11848b87437decb6381ed3ec840492b706 --data service=${service} --data version=${currentTag}'
                }
            }
        }
    }
}
