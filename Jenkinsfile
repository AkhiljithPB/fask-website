pipeline {

   agent any
   options {
       buildDiscarder(logRotator(numToKeepStr: '5'))   
   }

   environment {
       DOCKERHUB_CREDENTIALS = credentials('akhiljith-dockhub')
   }
   stages {
       stage('Build') {
           steps {
               sh 'docker build -t akhiljith/flask-app:latest .'
           }
       }
       stage('Login') {
           steps {
               sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
           }
       }
       stage('push') {
           steps {
               sh 'docker push akhiljith/flask-app:latest'
           }
       }
   }
   post {
       always {
           sh 'docker logout'
       }
   }
}
