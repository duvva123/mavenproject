pipeline {
    agent any

    stages {
        stage('Build') {
            agent { label 'slave' }
            steps {
                echo 'Building..'
                sh '''
                   cd /home/ubuntu/
                   pwd
                   ansible node -m ping
                   cd /home/ubuntu/playbook/	  
                   ansible-playbook deploy.yaml
                   cd /home/ubuntu/playbook/
                '''
            }
        }

        stage('Compile Stage') {
            steps {
                sh "sudo /home/ubuntu/playbook/ mvn clean compile"
            }
        }
        stage('Package') {
            steps {
                sh "mvn package"
            }
        }
    }
}
