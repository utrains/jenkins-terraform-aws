pipeline {
     agent any
        
     stages {
         stage('Checkout') {
             steps {
                 git branch: 'main', url: 'https://github.com/utrains/jenkins-terraform-aws'
             }
         }
         stage('Checkov') {
             steps {
                 script {
                     docker.image('bridgecrew/checkov:latest').inside("--entrypoint=''") {
                         try {
                             sh 'checkov -d . --use-enforcement-rules -o cli -o junitxml --output-file-path console,results.xml --repo-id utrains/jenkins-terraform-aws --branch main --bc-api-key 271cfa61-a5b2-41fd-a7c7-68f43a437daf'
                             junit skipPublishingChecks: true, testResults: 'results.xml'
                         } catch (err) {
                             junit skipPublishingChecks: true, testResults: 'results.xml'
                             throw err
                         }
                     }
                 }
             }
         }
     }
     options {
         preserveStashes()
         timestamps()
     }
 }