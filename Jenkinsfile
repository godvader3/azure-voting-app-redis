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
      stage('Approve Stg Deploy') {
         when {
            branch 'stg'
         }
         options {
            timeout(time: 1, unit: 'HOURS')
         }
         steps {
            input message: "Deploy?"
         }
         post {
            success {
               echo "Stg Deploy Approved"
            }
            aborted {
               echo "Stg Deploy Denied"
            }
         }
      }
      stage('Deploy to Stg') {
         when {
            branch 'stg'
         }
         environment {
            ENVIRONMENT = 'stg'
         }
         steps {
            echo "Deploying to ${ENVIRONMENT}"
            echo "Test for stg env only successfull"
         }
      }
   }
}
