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
	       sshPublisher(publishers: [sshPublisherDesc(configName: 'ansible', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /home/ansadmin/docker;''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/docker', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '**'), 
	       sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /home/ansadmin/docker; echo "I did it" > /home/ansadmin/docker/ididit.txt; echo "I did it again" > /home/ansadmin/docker/ididitagain.txt; ''', flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '', usePty: true)], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
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
            echo "Test for dev env only successfull"
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
            echo "Test for stg env only successfull..."
         }
      }
   }
}
