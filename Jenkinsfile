pipeline {
   agent {
       label 'docker-gobuild'
   }
    
   stages {
      stage('Get code') {
         steps {
            // Get some code from a GitHub repository
            git 'https://github.com/PiterPentester/go_test.git'
         }
      }
      stage('Build') {
         steps {
            sh 'go build main.go'
         }
      }
      stage('Run') {
         steps {
            sh './main'
         }
      }
   }
}
