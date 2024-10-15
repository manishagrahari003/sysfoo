pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Building'
        sh 'mvn compile'
      }
    }

    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            echo 'test'
            sh 'mvn clean test'
          }
        }

        stage('unit') {
          steps {
            sleep 2
          }
        }

        stage('UI') {
          steps {
            sleep 5
          }
        }

      }
    }

    stage('Package') {
      steps {
        echo 'package artifact'
        sh 'nvm package -DskipTests'
      }
    }

    stage('archive') {
      steps {
        archiveArtifacts '**/target/*.jar'
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