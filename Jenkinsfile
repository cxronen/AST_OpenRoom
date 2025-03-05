node {
  stage('SCM') {
    checkout scm
  }
  stage('Checkmarx Analysis') {
    writeFile file: 'cx_result_sonar.json', text: ''
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
