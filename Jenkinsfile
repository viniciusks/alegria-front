pipeline {
    agent any

    environment {
      NAME_FOLDER_ZIP = "source.zip"
    }

    stages {
        stage('Build') {
          steps {
            echo "Começou o build..."
            zip zipFile: NAME_FOLDER_ZIP,
                archive: false,
                exclude: '.git, .editorconfig, README.md, Jenkinsfile'
            sh 'ls -lah'
          }
        }
    }
}