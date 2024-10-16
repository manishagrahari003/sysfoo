pipeline {
  agent none
  stages {
    stage('Build') {
      agent {
        docker {
          image 'maven:3.9.6-eclipse-temurin-17'
        }

      }
      steps {
        echo 'Building'
        sh 'mvn compile'
      }
    }

    stage('Test') {
      parallel {
        stage('Test') {
          agent {
            docker {
              image 'maven:3.9.6-eclipse-temurin-17'
            }

          }
          steps {
            echo 'test'
            sh 'mvn clean test'
          }
        }

        stage('unit') {
          agent any
          steps {
            sleep 2
          }
        }

        stage('UI') {
          agent any
          steps {
            sleep 5
          }
        }

      }
    }

    stage('Package') {
      agent {
        docker {
          image 'maven:3.9.6-eclipse-temurin-17'
        }

      }
      steps {
        echo 'package artifact'
        sh 'mvn package -DskipTests'
      }
    }

    stage('archive') {
      agent {
        docker {
          image 'maven:3.9.6-eclipse-temurin-17'
        }

      }
      steps {
        archiveArtifacts '**/target/*.jar.original'
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