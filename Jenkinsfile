node {
  stage ('build') {
    openshiftBuild(buildConfig: 'nodejsci', showBuildLogs: 'true')
  }
  stage ('shall we go live?') {
    timeout(time:15, unit:'MINUTES') {
      input message: "Shall we go live?"
    }
  }
  stage ('deploy development') {
    openshiftDeploy depCfg: 'nodejsci'
    openshiftVerifyDeployment depCfg: 'nodejsci', replicaCount: 1, verifyReplicaCount: true
  }
  stage ('system test') {
    sh "curl -s http://nodejsci-myjenkins.os.hr4.local/ | grep 'Hello'"
  }
}
