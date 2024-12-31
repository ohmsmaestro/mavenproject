pipeline {
    agent any
    
    environment {
        ANSIBLE_CONFIG = '/etc/ansible/ansible.cfg'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'git@github.com:ohmsmaestro/1pally-service.git'
            }
        }
        
        stage('Build') {
            steps {
                sh './mvnw clean package -DskipTests'
            }
        }
        
        stage('Deploy with Ansible') {
            steps {
                ansiblePlaybook(
                    inventory: 'inventory',
                    playbook: 'deploy.yml'
                )
            }
        }
    }
    
    post {
        success {
            echo 'Deployment Successful!'
        }
        failure {
            echo 'Deployment Failed.'
        }
    }
}
