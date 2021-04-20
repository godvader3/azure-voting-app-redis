pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"

            sshPublisher(publishers: [sshPublisherDesc(configName: 'ansible', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /home/ansadmin/docker;''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/docker', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '**'),
	    sshTransfer(cleanRemote: false, excludes: '', execCommand: '''cd /home/ansadmin/docker; echo "I did it" > /home/ansadmin/docker/ididit-master.txt; echo "I did it again" > /home/ansadmin/docker/ididitagain-master.txt; ''', flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '', usePty: true)], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])	   
         }
      }
   }
}

