pipeline {
    agent {
        docker {
            image 'kennethreitz/pipenv'
            args '-u root --privileged -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Checkout') {
             steps {
                 git branch: 'main', url: 'https://github.com/utrains/jenkins-terraform-aws'
                //  stash includes: '**/*', name: 'jenkins-terraform-aws'
             }
         }
        stage('test') {
            steps {
                // checkout([$class: 'GitSCM', branches: [[name: 'main']], userRemoteConfigs: [[url: 'https://github.com/utrains/jenkins-terraform-aws.git']]])
                script { 
                    //sh "checkov -d . --use-enforcement-rules -o cli -o junitxml --output-file-path console,results.xml --repo-id utrains/jenkins-terraform-aws --branch main"
                    // sh """export BC_API_URL=https://www.bridgecrew.cloud
                    // pwd
                    // checkov -d /var/lib/jenkins/workspace/scan_terraform --bc-api-key 6283b629-b384-439a-9e58-90099438686a --repo-id utrains/jenkins-terraform-aws --branch main"""    

                    "export BC_API_URL=https://www.bridgecrew.cloud" 
                    "checkov -d jenkins-terraform-aws --bc-api-key 1e106f9c-96de-4380-89c0-50c0a8bb9110 --repo-id utrains/jenkins-terraform-aws --branch main"
                    
                }
            }
        }
    }
    options {
        preserveStashes()
        timestamps()
    }
}
// pipeline {
//      agent any
        
//      stages {
//          stage('Checkout') {
//              steps {
//                  git branch: 'main', url: 'https://github.com/utrains/jenkins-terraform-aws'
//                  stash includes: '**/*', name: 'jenkins-terraform-aws'
//              }
//          }
//          stage('Checkov') {
//              steps {
//                  script {
//                     //  docker.image('bridgecrew/checkov:latest').inside("--entrypoint=''") {
//                     //      unstash 'terragoat'
//                          try {
//                              sh 'checkov -d . --use-enforcement-rules -o cli -o junitxml --output-file-path console,results.xml --repo-id utrains/jenkins-terraform-aws --branch main'
//                              junit skipPublishingChecks: true, testResults: 'results.xml'
//                          } catch (err) {
//                              junit skipPublishingChecks: true, testResults: 'results.xml'
//                              throw err
//                          }
//                     //  }
//                  }
//              }
//          }
//      }
//      options {
//          preserveStashes()
//          timestamps()
//      }
//  }
// pipeline {
//      agent any
        
//      stages {
//          stage('Checkout') {
//              steps {
//                  git branch: 'main', url: 'https://github.com/utrains/jenkins-terraform-aws'
//                  stash includes: '**/*', name: 'jenkins-terraform-aws'
//              }
//          }
//          stage('Checkov2') {
//              steps {
//                  script {
//                     // sh "pipenv run pip install checkov"
//                     sh "ls"
//                     // sh "pipenv run checkov -d . --use-enforcement-rules -o cli -o junitxml --output-file-path console,results.xml --repo-id utrains/jenkins-terraform-aws --branch main"
//                  }
//              }
//          }
//      }
//      options {
//          preserveStashes()
//          timestamps()
//      }
//  }