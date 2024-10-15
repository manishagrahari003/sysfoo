pipeline {
  agent any
  stages {
    stage('one') {
      steps {
        echo 'Building'
        sh 'mvn compile'
      }
    }

    stage('two') {
      steps {
        echo 'test'
        sh 'mvn clean test'
      }
    }

    stage('three') {
      steps {
        echo 'step 3'
        sleep 5
      }
    }

  }
  tools {
    maven 'Maven 3.6.3'
  }
  post {
    always {
      echo 'This pipeline is completed..'
    }

  }
}