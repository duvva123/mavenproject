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
       stage('Compile') {
            agent { label 'slave' }
            steps {
                echo 'Compile..'
                sh '''
                cd /home/ubuntu/playbook/
                sudo mvn compile
                '''
            }
        }
    post {
       failure {
            script {
                currentBuild.result = 'FAILURE'
            }
        }

       always {
            step([$class: 'Mailer',
                notifyEveryUnstableBuild: true,
                recipients: "duvva.raghavendra@gmail.com",
                sendToIndividuals: true])
        } 
     }
   }    
}
