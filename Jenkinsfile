pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "mymaven"
    }

    stages {
        stage('build maven') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'gitcredential', url: 'https://github.com/dmrichey/FullstackExample']])
                bat "mvn clean install"
            }
        }
        
        stage('build docker image') {
            steps{
                script{
                    bat 'docker build -t dmrichey/myjenkins .'
                }
            }
        }
        
        stage('push docker image to docker hub') {
            steps{
                script{
                    withCredentials([string(credentialsId: 'mydockerhubpassword', variable: 'mydockerhubpassword')]) {
                        bat 'docker login -u richeydm.dev@gmail.com -p !246ad%Two docker.io'
                        
                        bat 'docker push dmrichey/myjenkins'
                    }
                }
            }
        }
    }
}