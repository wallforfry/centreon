stage('Source') {
  node {
    dir('centreon-web') {
      checkout scm
    }
    xunit (
      thresholds: [ skipped(failureThreshold: '0'), failed(failureThreshold: '0') ],
      tools: [Custom(customXSL: 'centreon-web/junit.xsd', pattern: 'centreon-web/xunit-reports/**/*.xml') ]
    )
  }
}
if ((currentBuild.result ?: 'SUCCESS') != 'SUCCESS') {
  error('Critical tests stage failure.');
}
