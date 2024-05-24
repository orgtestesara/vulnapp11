pipeline {
    agent any
    //tools {
      //  sonar 'SonarScanner' // Nome configurado anteriormente para o SonarScanner
    //}
    environment {
        SONAR_HOST_URL = 'http://54.175.178.217:9001' // URL do seu servidor SonarQube
        SONAR_AUTH_TOKEN = credentials('squ_31a956424e72e785f59b8cd60942720e4f19a53c') // ID da credencial do token configurado no Jenkins
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
