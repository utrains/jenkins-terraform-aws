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
                    pwd"""
                    
                }
            }
        }
    }
    options {
        preserveStashes()
        timestamps()
    }
}