pipeline {
  agent any
  stages {
    stage('First Stage') {
      steps {
        parallel(
          "First Stage": {
            sh 'echo "Hello world"'
            
          },
          "Parallel First": {
            sh 'echo "parallel first"'
            
          }
        )
      }
    }
    stage('Second Stage') {
      steps {
        sh 'echo "second step"'
      }
    }
  }
}