node {
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'VMSonar';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
  stage('Checkmarx Analysis') {
    checkmarxASTScanner additionalOptions: '--report-format sonar', baseAuthUrl: '', branchName: 'master', checkmarxInstallation: 'CxCLI', credentialsId: '', projectName: 'AST_OpenRoom_jenkins', serverUrl: '', tenantName: '', useOwnAdditionalOptions: true
  }
}
