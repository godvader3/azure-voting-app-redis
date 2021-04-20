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
	       sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /home/ansadmin/docker; echo "I did it" > /home/ansadmin/docker/ididit-dev.txt; echo "I did it again" > /home/ansadmin/docker/ididitagain-dev.txt; ''', flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '', usePty: true)], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
            aborted {
               echo "Dev Deploy Denied"
            }
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
	       sshPublisher(publishers: [sshPublisherDesc(configName: 'ansible', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /home/ansadmin/docker;''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/docker', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '**'),
               sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /home/ansadmin/docker; echo "I did it" > /home/ansadmin/docker/ididit-stg.txt; echo "I did it again" > /home/ansadmin/docker/ididitagain-stg.txt; ''', flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '', usePty: true)], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
            aborted {
               echo "Stg Deploy Denied"
            }
         }
      }
   }
}
