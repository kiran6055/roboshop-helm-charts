pipeline {

  agent {
    label 'JenkinsAgent'
  }
  parameters {
    string(name: 'COMPONENT', defaultValue: '', description: 'Enter COMPONENT')
    string(name: 'APP_VERSION', defaultValue: '', description: 'APP_VERSION')

  }
  stages {

    stage ('Get APP File') {
      steps {
        dir('APP') {
          git branch: 'main', url: 'https://github.com/kiran6055/${COMPONENT}.git'
        }
        dir('HELM') {
          git branch: 'main', url: 'https://github.com/kiran6055/roboshop-helm-charts'
        }
      }

    }
    stage ('Helms Deploy') {
      steps {
        sh 'helm upgrade -i ${COMPONENT} ./HELM -f APP/values.yaml --set-string image.tag="${APP_VERSION},env=prod,COMPONENT=${COMPONENT}"'
      }
    }

  }

  post {
    always {
      cleanWs ()
    }
  }

}