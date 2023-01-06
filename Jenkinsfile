// pipeline {
//     agent {
//         docker {
//             image 'fsfe/pipenv:bitnami-3.8'
//             args '-u root --privileged -v /var/run/docker.sock:/var/run/docker.sock'
//         }
//     }
//     stages {
//         stage('test') {
//             steps {
//                 checkout([$class: 'GitSCM', branches: [[name: 'master']], userRemoteConfigs: [[url: 'https://github.com/utrains/jenkins-terraform-aws.git']]])
//                 script { 
//                     sh """pipenv install
//                     pipenv run pip install bridgecrew
//                     pipenv run bridgecrew --directory . --bc-api-key 271cfa61-a5b2-41fd-a7c7-68f43a437daf --repo-id utrains/jenkins-terraform-aws"""
//                 }
//             }
//         }
//     }
//     options {
//         preserveStashes()
//         timestamps()
//     }
// }
pipeline {
     agent any
        
     stages {
         stage('Checkout') {
             steps {
                 git branch: 'main', url: 'https://github.com/utrains/jenkins-terraform-aws'
                 //stash includes: '**/*', name: 'jenkins-terraform-aws'
             }
         }
         stage('Checkov') {
             steps {
                 script {
                     docker.image('bridgecrew/checkov:latest').inside("--entrypoint=''") {
                         unstash 'jenkins-terraform-aws'
                         try {
                             sh 'checkov -d . --use-enforcement-rules -o cli -o junitxml --output-file-path console,results.xml --repo-id utrains/jenkins-terraform-aws --branch main'
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