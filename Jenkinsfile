pipeline {
  agent any 
  stages {
    stage("Testing maven"){
      steps{
        sh """mvn -version"""
      }
    }
    
    stage ("build") {
      steps {
        echo 'building the application...' 
      }
    }

    stage ("test") {
      steps {
          echo 'testing the application...'
      }
    }

    stage ("deploy") {
      steps{
        echo 'deplying the application...'
      }
    }
  }
}
