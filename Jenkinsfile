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
                    withCredentials([usernamePassword(credentialsId: 'DockerHub', passwordVariable: 'PASS' , usernameVariable: 'USER')]) {
                       sh "docker build -t snegi2020/demo-app:${IMAGE_NAME} ."
                       sh "echo $PASS | docker login -u $USER --password-stdin "
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
        stage('Commiting Version Update to GitHub') {
            steps {
                script{
                    echo 'Comitting to Github repo '
                    withCredentials([usernamePassword(credentialsId: 'mygithub-cred', passwordVariable: 'PASS' , usernameVariable: 'USER')]) {
                       sh 'git config user.email "negi.supriya88@gmail.com"'
                       sh 'git config user.name "sn2020"'
                       sh 'git config credential.helper store'
                       sh 'git status'
                       sh 'git branch'
                       sh 'git config --list'
                       //sh "echo $PASS"
                       sh "echo $PASS | git remote set-url origin https://$USER:--password-stdin@github.com/sn2020/jenkins-bootcamp.git" 
                       sh "pwd"
                       sh "git add ."
                       sh 'git commit -m "version patched"'
                       sh "git push origin HEAD:main"
                    }
                }
            }
        }
    }
}