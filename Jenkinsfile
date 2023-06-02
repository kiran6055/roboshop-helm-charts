pipeline {

  agent {
    label 'JenkinsAgent'
  }
  parameters {
    string(name: 'component', defaultValue: '', description: 'Enter component')
    string(name: 'app_version', defaultValue: '', description: 'app_version')

  }
  stages {

    stage ('get values file') {
      steps {
        dir('APP') {
          git branch: 'main', url: 'https://github.com/kiran6055/${component}.git'
        }
      }

    }
    stage ('Helms file') {
      steps {
        sh 'helm upgrade -i ${component} . -f APP/values.yaml --set-string image.tag=${app_version}'
      }
    }

  }

}