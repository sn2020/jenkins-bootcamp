pipeline {
    agent any
    
    //environment {
      //  IMAGE_NAME = 'sn2020/demo-app:java-npm-app-1.0'
    //}
    stages {
        stage('Build') {
            steps {
               script {
                  echo 'Building nodejs'
                  dir ('app') { 
                    sh "pwd"
                    sh "npm install" 
                    sh 'npm version major'
                    props = readJSON file: 'package.json'
                    echo props.version
                    env.IMAGE_NAME = "$props.version-${BUILD_NUMBER}"
                    echo "${BUILD_NUMBER}"
                    
                    }
                }
            }
        }
        
        stage('Test...') {
            steps {
               script {
                  echo 'test application jar...'
                  dir ('app') {
                    sh 'npm test'
                  }
                }
            }
        }
        
        stage('Building Docker Image') {
            steps {
                script {
                    echo 'building docker image'
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS' , usernameVariable: 'USER')]) {
                       sh "docker build -t snegi2020/demo-app:${IMAGE_NAME} ."
                       sh "echo $PASS | docker login -u $USER --passowrd-stdin "
                       sh "docker push snegi2020/demo-app:${IMAGE_NAME}" 
                       echo "Pushed Docker Image successfuuly ${IMAGE_NAME}"
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