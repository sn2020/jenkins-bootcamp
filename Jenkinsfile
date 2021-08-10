pipeline {
    agent any
    
    environment {
        IMAGE_NAME = 'sn2020/demo-app:java-npm-app-1.0'
    }
    stages {
        stage ('increment version'){
            steps {
                script{
                    echo "This is the current path ${pwd}"
                    echo 'incrementing major version'
                    cd ./app
                    echo "This is the new path ${pwd}"
                    sh 'npm version major'
                }
            }
        }
        stage('test app') {
            steps {
               script {
                  echo 'test application jar...'
                  sh 'npm test'
                }
            }
        }
        stage('build image') {
            steps {
                script {
                   echo 'building docker image...'
                   withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS' , usernameVariable: 'USER')]) {
                        sh 'docker build -t snegi2020/demo-app:image-1.0 .'
                        sh "echo $PASS | docker login -u $USER --passowrd-stdin "
                        sh 'docker push snegi2020/demo-app:image-1.0 '
                    }
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
