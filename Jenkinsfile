pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            echo $GIT_BRANCH
         }
      }

      stage('Docker Build') {
         steps {
	    sh label: '', script: '''cd azure-vote/
			ls -l
			echo lapar'''
         }
      }  
   }
}
