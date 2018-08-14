stage('Source') {
  node {
    dir('centreon-web') {
      checkout scm
    }
    junit 'centreon-web/xunit-reports/**/*.xml'
  }
}
if ((currentBuild.result ?: 'SUCCESS') != 'SUCCESS') {
  error('Critical tests stage failure.');
}
