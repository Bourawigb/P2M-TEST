pipeline {
   agent any
   environment {
    DOCKERHUB_CREDENTIALS = credentials('06decbaf-b4e6-4429-8cd3-0778dfa98a25')
    }
   triggers {
        pollSCM "*/5 * * * *"
    }

   stages {

      stage('Build Image') {
         steps {
           sh '''
           docker build -t bourawi/p2m .
           '''
         }
      }

    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }

      stage('Push Image') {
         steps {
           sh '''
           docker push bourawi/p2m
           '''
         }
      }
   }
   post {
    always {
      sh 'docker logout'
    }
  }
}