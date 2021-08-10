pipeline {
    agent any
    
    environment {
        IMAGE_NAME = 'sn2020/demo-app:java-npm-app-1.0'
    }
    stages {
        stage('increment version') {
            steps {
               script {
                  echo 'increment version...'
                  dir ('app') {
                    sh 'pwd'
                    sh 'npm version major'
                  }
                  //sh 'npm version major'
                }
            }
        }
        
        stage('test app') {
            steps {
               script {
                  echo 'test application jar...'
                  dir ('app') {
                    sh 'npm test'
                  }
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