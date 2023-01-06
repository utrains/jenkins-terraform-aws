pipeline {
    agent {
        docker {
            image 'kennethreitz/pipenv'
            args '-u root --privileged -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('test') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'main']], userRemoteConfigs: [[url: 'https://github.com/utrains/jenkins-terraform-aws.git']]])
                script { 
                    sh """export BC_API_URL=https://www.bridgecrew.cloud 
                    checkov -d main --bc-api-key 6283b629-b384-439a-9e58-90099438686a --repo-id utrains/jenkins-terraform-aws --branch main"""
                }
            }
        }
    }
    options {
        preserveStashes()
        timestamps()
    }
}