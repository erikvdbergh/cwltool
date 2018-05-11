pipeline {
  agent {
    node {
      label 'windows'
    }
  environment {
    CODECOV_TOKEN = credentials('jenkins-codecov-tokeN')
  }

  }
  stages {
    stage('build') {
      steps {
        withPythonEnv(pythonInstallation: 'Windows-CPython-36') {
          pybat '.jenkins/test.bat'
        }
      }
    stage('CWL-conformance-test') {
      steps {
        git 'https://github.com/common-workflow-language/common-workflow-language.git'
        withPythonEnv(pythonInstallation: 'Windows-CPython-36') {
          pybat '.jenkins/conformance-test.bat'
        }
      }
    }
  }
  post {
    always {
      junit 'tests.xml,**/conformance.xml'

    }

  }
}
