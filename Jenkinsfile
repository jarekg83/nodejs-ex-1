node {
  stage ('build') {
    openshiftBuild(buildConfig: 'nodejsci', showBuildLogs: 'true')
  }
  stage ('deploy development') {
    openshiftDeploy depCfg: 'nodejsci'
    openshiftVerifyDeployment depCfg: 'nodejsci', replicaCount: 1, verifyReplicaCount: true
  }
  stage ('system test') {
    sh "curl -s http://nodejsci:8080/ | grep 'Hello'"
  }
}
