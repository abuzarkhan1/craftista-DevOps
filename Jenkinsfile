pipeline{
   agent any
   tools{
      maven 'Maven 3.9.6'
   }

   stages{
    stage("Voting Build"){
      steps{
        echo 'compiling the voting app...'
        dir('voting') {
          sh 'maven compile'
        }
      }
    }
  }

  post{
    always{
      echo 'completed the file'
   } 
  }  
}
