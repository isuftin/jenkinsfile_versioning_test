pipeline {
  agent {
      node {
          label 'team:makerspace'
      }
  }
  parameters {
        gitParameter name: 'BRANCH_TAG',
                     type: 'PT_BRANCH_TAG',
                     defaultValue: 'origin/master'
  }
  stages {
    stage('Clean Workspace') {
      steps{
        cleanWs()
      }
    }
    stage('Display version') {
      steps {
        echo 'master'
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
          echo 'catme.txt says...'
          cat ${WORKSPACE}/catme.txt
          '''
      }
    }
    stage('Env Vars') {
      steps {
        sh 'printenv'
      }
    }
  }
}
