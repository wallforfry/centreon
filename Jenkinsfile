stage('Source') {
  node {
    dir('centreon-web') {
      checkout scm
    }
    step([
      $class: 'XUnitBuilder',
      thresholds: [
        [$class: 'FailedThreshold', failureThreshold: '0'],
        [$class: 'SkippedThreshold', failureThreshold: '0']
      ],
      tools: [[$class: 'PHPUnitType', pattern: 'centreon-web/xunit-reports/**/*.xml']]
    ])
  }
}
if ((currentBuild.result ?: 'SUCCESS') != 'SUCCESS') {
  error('Critical tests stage failure.');
}
