pipeline {

  agent {
    label 'JenkinsAgent'
  }
  parameters {
    string(name: 'component', defaultValue: '', description: 'Enter component')
    string(name: 'app_version', defaultValue: '', description: 'app_version')

  }
  stages {

    stage ('Get APP File') {
      steps {
        dir('APP') {
          git branch: 'main', url: 'https://github.com/kiran6055/${component}.git'
        }
        dir('HELM') {
          git branch: 'main', url: 'https://github.com/kiran6055/roboshop-helm-charts'
        }
      }

    }
    stage ('Helms Deploy') {
      steps {
        sh 'helm upgrade -i ${component} ./HELM -f APP/values.yaml --set-string image.tag=${app_version}'
      }
    }

  }

  post {
    always {
      cleanWs ()
    }
  }

}