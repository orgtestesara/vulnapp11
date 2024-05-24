pipeline {
	agent any
	tools {
	    maven "MAVEN3"
	    jdk "OracleJDK11"
	}

	stages {
	    stage('Fetch code') {
            steps {
               git branch: 'main', url: 'https://github.com/orgtestesara/vulnapp11.git'
            }

	    }

	    stage('Build'){
	        steps{
	           sh 'mvn install -DskipTests'
	        }

	        post {
	           success {
	              echo 'Now Archiving it...'
	              archiveArtifacts artifacts: '**/target/*.war'
	           }
	        }
	    }

	    stage('UNIT TEST') {
            steps{
                sh 'mvn test'
            }
       }

       stage('Checkstyle Analysis'){
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
       }

       stage('Sonar Analysis') {
            environment {
                scannerHome = tool 'sonar5.0'
            }
            steps {
               withSonarQubeEnv('mysonar') {
                   sh '''/home/ec2-user/sonar-scanner-5.0.1.3006-linux/bin/sonar-scanner-5.0.1.3006-linux/bin/sonar-scanner -Dsonar.projectKey=my-project \
                   -Dsonar.projectName=my-project \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
              }
           }
       }

       stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
	}
}
