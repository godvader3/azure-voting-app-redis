pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
      }
      stage('Approve Dev or Stg Deploy') {
         when {
            branch 'dev' || 'stg'
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
      stage('Deploy to Dev or Stg') {
         when {
            branch 'dev' || 'stg'
         }
         steps {
            echo "Test for dev or stg env only successfull."
         }
      }
   }
}

