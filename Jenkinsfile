pipeline {
    agent any
    
    environment {
        ANSIBLE_CONFIG = '/etc/ansible/ansible.cfg'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/ohmsmaestro/mavenproject.git'
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
                    inventory: '/var/lib/jenkins/ansible/inventory',
                    playbook: '/var/lib/jenkins/ansible/deploymeny.yml'
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
