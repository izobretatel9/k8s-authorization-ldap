@Library('jenkins-devops@dev')_ // load jenkins-devops as a library

properties([
  parameters([
    choice(      name: 'TYPE',              choices: ['converge', 'dismiss'],
                                            defaultValue: 'converge',                description: 'TYPE of run Deploy or Dismis packages'),
    string(      name: 'SERVICE',           defaultValue: 'infra-authz',             description: 'Name of Service (also namespace too)'),
  ])
])

pipeline {
  agent { label 'werf' }

  environment {
//  WERF_REPO               = "cr.yandex/xxxxxxxx/${params.SERVICE}" // if necessary
//  WERF_STAGES_STORAGE     = "cr.yandex/xxxxxxxx/${params.SERVICE}/stages" // if necessary
    WERF_TMP_DIR            = '/home/jenkins/tmp/'
    WERF_HOME               = '/home/jenkins/tmp/.werf/'

    KUBECONFIG              = credentials('werf_devops_kube_config')
    WERF_SECRET_KEY         = credentials("werf_secret_key")
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage("Prerequisites") {
      steps {
        script {
          sh 'export'
        }
      }
    }
    stage("PROD") {
      when {
        anyOf { branch 'master'; }
      }
      environment {
        WERF_NAMESPACE        = "${params.SERVICE}"
        WERF_ENV              = "prod"
        WERF_KUBE_CONTEXT     = "devops-prod" // change
      }
      steps {
        script {
          functions.runWerf("${params.TYPE}", "1.2 beta")
        }
      }
    }
  }
}
