pipeline {
  agent none
  stages {
    stage('Voting Build') {
      agent {
        docker {
          image 'maven:4-eclipse-temurin-19-alpine'
        }

      }
      steps {
        echo 'Compiling the voting app...'
        dir(path: 'voting') {
          sh 'mvn compile'
        }

      }
    }

    stage('Voting Test') {
      steps {
        dir(path: 'voting') {
          sh 'mvn clean test'
        }

      }
    }

    stage('Voting package') {
      parallel {
        stage('Voting package') {
          steps {
            dir(path: 'voting') {
              sh 'mvn package -DskipTests'
            }

            archiveArtifacts '**/target/*jar'
          }
        }

        stage('Voting Image ') {
          agent any
          steps {
            script {
              docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
                def commitHash = env.GIT_COMMIT.take(7)
                def dockerImage = docker.build("abuzarkhan1/craftista-voting:${commitHash}", "./")
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
    maven 'Maven 3.9.9'
  }
  post {
    always {
      echo 'Pipeline execution completed.'
    }

  }
}