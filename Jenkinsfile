stage('Source') {
  node {
    dir('centreon-web') {
      checkout scm
    }
    script {
      def testResults = findFiles(glob: 'centreon-web/xunit-reports/**/*.xml')
      for(xml in testResults) {
        touch xml.getPath()
      }
    }
    junit 'centreon-web/xunit-reports/**/*.xml'
  }
}
if ((currentBuild.result ?: 'SUCCESS') != 'SUCCESS') {
  error('Critical tests stage failure.');
}
