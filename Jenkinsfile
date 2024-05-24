node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'SonarScanner';
    withSonarQubeEnv() {
      sh "/home/ec2-user/sonar-scanner-5.0.1.3006-linux/bin/sonar-scanner"
    }
  }
}
