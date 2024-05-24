pipeline {
    agent any
    //tools {
      //  sonar 'SonarScanner' // Nome configurado anteriormente para o SonarScanner
    //}
    environment {
        SONAR_HOST_URL = 'http://54.175.178.217:9001' // URL do seu servidor SonarQube
        SONAR_AUTH_TOKEN = credentials('sonar-token-id'') // ID da credencial do token configurado no Jenkins
    }
    stages {
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube Server') { // Nome configurado para o servidor SonarQube
                    sh 'sonar-scanner -Dsonar.login=$SONAR_AUTH_TOKEN'
                }
            }
        }
    }
}
