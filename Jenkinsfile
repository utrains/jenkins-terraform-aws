pipeline {
    agent {
        docker {
            image 'kennethreitz/pipenv:latest'
            args '-u root --privileged -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('test') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'master']], userRemoteConfigs: [[url: 'https://github.com/utrains/jenkins-terraform-aws.git']]])
                script { 
                    sh """pipenv install
                    pipenv run pip install bridgecrew
                    pipenv run bridgecrew --directory . --bc-api-key 05ef6658-1ce5-4f4c-ab0a-688f490bf56d --repo-id utrains/jenkins-terraform-aws"""
                }
            }
        }
    }
    options {
        preserveStashes()
        timestamps()
    }
}