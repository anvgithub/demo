pipeline {
    agent any

    stages {
        stage('Install Docker and Docker-compose') {
            steps {
                   ansiblePlaybook become: true, credentialsId: 'ansible', 
                   installation: 'ansible', inventory: '/home/anv/inventory', 
                   limit: 'dev', playbook: '/home/anv/ansible-playbooks/docker_ubuntu1804/playbook.yml'  
            }
        }
    }
}