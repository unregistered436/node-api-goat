pipeline {
  agent any
  environment {
      HOME = '.'
  }
  stages {
    stage('Build') {
      steps {
        sh 'rm -rf node_modules && npm install'
      }
    }
    stage('Test') {
      steps {
        wrap([$class: 'VeracodeInteractiveBuildWrapper', location: 'iast-jenkins.pmcneil.sa.veracode.io', port: '10010']) {

          sh 'curl -sSL https://s3.us-east-2.amazonaws.com/app.veracode-iast.io/iast-ci.sh | sh'
          sh 'LD_LIBRARY_PATH=$WORKSPACE npm run test-iast'
        }
      }
    }
    stage('Deploy') {
      steps {
        sh 'echo npm package would run here...'
      }
    }
  }
}
