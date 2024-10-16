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
        if (env.BRANCH_NAME !== 'main') {
          return
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
      parallel {
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

        stage('Docker bP') {
          agent any
          steps {
            script {
              docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
                def commitHash = env.GIT_COMMIT.take(7)
                def dockerImage = docker.build("manish7863/sysfoo:${commitHash}", "./")
                dockerImage.push()
                dockerImage.push("latest")
                dockerImage.push("dev")
              }
            }

          }
        }

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
