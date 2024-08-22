pipeline {
    agent any
    tools {
        maven 'Maven 3.9.6'
    }

    stages {
        stage("Voting Build") {
            steps {
                echo 'Compiling the voting app...'
                dir('voting') {
                    sh 'mvn compile'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
    }
}
