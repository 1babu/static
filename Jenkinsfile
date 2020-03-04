pipeline {
     agent any
     stages {
          stage('Lint HTML') {
              steps {
                  sh 'tidy -q -e *.html'
              }
         }
          
         stage('Upload to AWS') {
             steps {
                 withAWS(region:'us-east-2',credentials:'aws-static') {
                 sh 'echo "Uploading content with AWS creds"'
                     s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'cicd-udacity')
                 }
             }
         stage('Check URL') {
             steps {
                 sh '''
                     echo "Test website URL access"
                     curl -s -o /dev/null  http://cicd-udacity.s3-website.us-east-2.amazonaws.com/ ; ec=$?; echo $ec
                 '''
             }
         }
     }
}
