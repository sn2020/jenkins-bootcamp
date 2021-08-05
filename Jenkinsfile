pipeline {
    agent any
    
    environment {
        IMAGE_NAME = 'sn2020/demo-app:java-npm-app-1.0'
    }
    stages {
        stage('build app') {
            steps {
               script {
                  echo 'building application jar...'
                }
            }
        }
        stage('build image') {
            steps {
                script {
                   echo 'building docker image...'
                   //buildImage(env.IMAGE_NAME)
                   //dockerLogin()
                   //dockerPush(env.IMAGE_NAME)
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                   echo 'deploying docker image to EC2...'
                }
            }
        }
    }
}
