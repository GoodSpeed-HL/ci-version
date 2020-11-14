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
                sh 'docker build -t helloworld:${currentTag} .'
                sh 'docker tag helloworld:${currentTag} registry.digitalocean.com/bitcoco/helloworld:${currentTag}'
                sh 'docker push registry.digitalocean.com/bitcoco/helloworld:${currentTag}'
            }
        }

        stage('post'){
             steps {
                sh 'curl https://bot:11848b87437decb6381ed3ec840492b706@pipelines.bitcoco.ca/job/short-test/buildWithParameters?token=Fa89vNYgsjZF7k4L&service=${service}&version=${currentTag}'
            }
            
        }
    }
}
