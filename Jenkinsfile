pipeline {
  agent {
      node {
          label 'team:makerspace'
      }
  }
  parameters {
        gitParameter name: 'BRANCH_TAG',
                     type: 'PT_BRANCH_TAG',
                     defaultValue: 'master'
  }
  stages {
    stage('Clean Workspace') {
      steps{
        cleanWs()
      }
    }
    stage('Display version') {
      steps {
        echo '0.0.1'
      }
    }
    stage('Checkout repo and pull model output from S3') {
      steps {
        checkout([$class: 'GitSCM',
                          branches: [[name: "${params.BRANCH_TAG}"]],
                          doGenerateSubmoduleConfigurations: false,
                          extensions: [],
                          gitTool: 'Default',
                          submoduleCfg: [],
                          userRemoteConfigs: [[url: 'https://github.com/isuftin/jenkinsfile_versioning_test']]
                        ])

        sh '''
          sh 'catme.txt says...'
          cat catme.txt
          '''
      }
    }
  }
    post {
        success {
            sh 'success'
        }
        unstable {
            sh 'unstable'
        }
        failure {
            sh 'failure'
        }
        changed {
            sh 'changed'
        }
    }
}
