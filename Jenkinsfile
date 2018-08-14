stage('Source') {
  parallel 'centos6': {
    node {
      dir('centreon-web') {
        checkout scm
      }
      stash includes: 'centreon-web/xunit-reports/centos6/**', name: 'xunit-reports-centos6'
    }
  },
  'centos7': {
    node {
      dir('centreon-web') {
        checkout scm
      }
      stash includes: 'centreon-web/xunit-reports/centos7/**', name: 'xunit-reports-centos7'
    }
  }

  unstash 'xunit-reports-centos6'
  unstash 'xunit-reports-centos7'
  script {
    def testResults = findFiles(glob: 'centreon-web/xunit-reports/**/*.xml')
    for(xml in testResults) {
      touch xml.getPath()
    }
  }
  junit 'centreon-web/xunit-reports/**/*.xml'
}
if ((currentBuild.result ?: 'SUCCESS') != 'SUCCESS') {
  error('Critical tests stage failure.');
}
