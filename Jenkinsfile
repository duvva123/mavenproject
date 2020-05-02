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
                echo 'Building..'
                sh '''
                   cd /home/ubuntu/
                   pwd
                   sh "mvn clean compile"
                ...
            }
        }
        stage('Package') {
            steps {
                echo 'Building..'
                sh '''
                   cd /home/ubuntu/
                   pwd
                   sh "mvn package"
                ...
            }
        }
    }
}
