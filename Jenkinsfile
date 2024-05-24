pipeline {
    agent any
    
    environment {
        SONAR_TOKEN = credentials('JENKINS_URL/job/proj1/build?token=JENKINS_TOKEN1')
    }
    
    stages {
        stage('SonarQube Analysis') {
            steps {
                // Executar a análise com SonarQube Scanner
                withSonarQubeEnv('SonarQube Server') {
                    sh "/home/ec2-user/sonar-scanner-5.0.1.3006-linux/bin/sonar-scanner-5.0.1.3006-linux/bin/sonar-scanner -Dsonar.login=$SONAR_TOKEN"
                }
            }
        }
    }
    
    post {
        always {
            // Notificar o resultado da análise no console
            script {
                echo 'Análise do SonarQube concluída.'
            }
        }
    }
}
