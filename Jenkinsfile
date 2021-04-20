pipeline {
   agent any

   stages {
      stage('Verify Branch') {
         steps {
            echo "$GIT_BRANCH"
         }
      }
      stage('Docker Build') {
         steps {
            sh label: '', script: '''docker images -a
                        cd azure-vote/
                        docker images -a
                        docker build -t jenkins-pipeline .
                        docker images -a
                        cd ..
                        '''
            }
      stage('Start test app') {
        steps {
            sh label: '', script: """
            docker-compose up -d
            ./scripts/test_container.sh
        """)
         }
         post {
            success {
               echo "App started successfully :)"
            }
            failure {
               echo "App failed to start :("
            }
         }
      }
      stage('Run Tests') {
         steps {
            sh label: '', script: """
               pytest ./tests/test_sample.py
            """)
         }
      }
      stage('Stop test app') {
         steps {
            sh label: '', script: """
               docker-compose down
            """)
         }
      }     
   }
}

