pipeline {
    agent any
    
    //environment {
      //  IMAGE_NAME = 'sn2020/demo-app:java-npm-app-1.0'
    //}
    stages {
        stage('increment version') {
            steps {
               script {
                  echo 'increment version...'
                  dir ('app') {
                    sh 'pwd'
                    sh 'npm version major'
                    //def matcher = readFile('package.json') =~ '"version": (.+)'
                    //echo ${matcher}
                    //def version = matcher[0][1]
                    //echo ${version}
                    //env.IMAGE_NAME = "$version-$BUILD_NUMBER"
                    def currrentversion = {sh 'npm run env'} | {grep 'npm_package_version'} | {cut -d '=' -f 2}
                    echo ${currrentversion}
                  }
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
        
        stage('docker image build') {
            steps {
                script {
                    echo 'building docker image'
                    //withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS' , usernameVariable: 'USER')]) {
                       //sh "docker build -t snegi2020/demo-app:${IMAGE_NAME} ."
                       //sh "echo $PASS | docker login -u $USER --passowrd-stdin "
                       //sh "docker push snegi2020/demo-app:${IMAGE_NAME}" 
                    //}                
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