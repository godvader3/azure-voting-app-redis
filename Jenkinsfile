pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
      }
      stage('Approve Dev Deploy') {
         when {
            branch 'dev'
         }
         options {
            timeout(time: 1, unit: 'HOURS')
         }
         steps {
            input message: "Deploy?"
         }
         post {
            success {
               echo "Dev Deploy Approved"
            }
            aborted {
               echo "Dev Deploy Denied"
            }
         }
      }
      stage('Deploy to Dev') {
         when {
            branch 'dev'
         }
         environment {
            ENVIRONMENT = 'dev'
         }
         steps {
            echo "Deploying to ${ENVIRONMENT}"
            echo "Test for dev env only successfull."
         }
      }
   }
}

