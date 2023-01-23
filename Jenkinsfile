pipeline {
    agent any

    stages {
        stage('Build') {
          echo 'Começou o build...'
          zip zipFile: 'source.zip',
              archive: false,
              exclude: '.editorconfig README.md Jenkinsfile'
          sh 'ls -lah'
        }
    }
}