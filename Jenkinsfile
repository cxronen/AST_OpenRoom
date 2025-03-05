node {
  stage('SCM') {
    checkout scm
  }
  stage('Checkmarx Analysis') {
    sh "sudo type cx_result_sonar.json"
    sh "chmod 777 cx_result_sonar.json"
    //sh "chmod 777 ${env.WORKSPACE}"
    checkmarxASTScanner additionalOptions: '--scan-types sast --report-format sonar', baseAuthUrl: '', branchName: 'master', checkmarxInstallation: 'CxCLI', credentialsId: '', projectName: 'AST_OpenRoom_jenkins', serverUrl: '', tenantName: '', useOwnAdditionalOptions: true
  }
  stage('SonarQube Analysis') {
    def scannerHome = tool 'VMSonar';
    withSonarQubeEnv() {
      sh "${scannerHome}/bin/sonar-scanner"
    }
  }
}
