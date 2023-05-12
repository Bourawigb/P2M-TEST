pipeline {
   agent any
   environment {
    DOCKERHUB_CREDENTIALS = credentials('docker')
    }
   triggers {
        pollSCM "*/5 * * * *"
    }

   stages {

      stage('Build Image') {
         steps {
           sh '''
           docker build --network=host -t bourawi/p2m:$BUILD_NUMBER .
           '''
         }
      }
      stage('TEST phase') {
         steps {
           sh '''
           echo "testing...."
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
           docker push bourawi/p2m:$BUILD_NUMBER
           '''
         }
      }
      stage('Deleting Image') {
         steps {
           sh '''
           docker rmi -f bourawi/p2m:$BUILD_NUMBER
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