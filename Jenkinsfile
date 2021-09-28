pipeline {
    agent any

    stages {
        stage('Install Docker and Docker-compose') {
            steps {
                   ansiblePlaybook credentialsId: 'ansible', 
                   installation: 'ansible', inventory: '/home/anv/inventory', 
                    playbook: '/home/anv/playbook-docker.yml'  
            }
        }
        stage('Git clone') {
            steps {
                   ansiblePlaybook credentialsId: 'ansible', 
                   installation: 'ansible', inventory: '/home/anv/inventory', 
                    playbook: '/home/anv/git.yml'  
            }
        }

        stage('Build app') {
            steps {
                   ansiblePlaybook credentialsId: 'ansible', 
                   installation: 'ansible', inventory: '/home/anv/inventory', 
                    playbook: '/home/anv/build.yml'  
            }
        }
        
        stage('Deploy  to DEV _Stage') {
            steps {
                   ansiblePlaybook credentialsId: 'ansible', 
                   installation: 'ansible', inventory: '/home/anv/inventory', 
                    limit: 'dev', playbook: '/home/anv/deployapp.yml'  
            }
        }

        stage('Waiting for Approval'){
            steps {
                timeout(time: 40, unit: 'MINUTES') {
                    input (message: "Do you agree to deploy in the PROD?")
                }
            }
        
        }
        
        stage('Deploy  to PROD') {
            steps {
                   ansiblePlaybook credentialsId: 'ansible', 
                   installation: 'ansible', inventory: '/home/anv/inventory', 
                    limit: 'prod', playbook: '/home/anv/deployapp.yml'  
            }
        }


    }
}