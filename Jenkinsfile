def nameFolderZip = "source.zip"

pipeline {
    agent any

    environment {
      BRANCH_NAME = env.BRANCH_NAME
    }

    stages {
        stage('Build') {
          steps {
            echo "Começou o build da branch ${BRANCH_NAME}..."
            zip zipFile: nameFolderZip,
                archive: false,
                exclude: '.git, .editorconfig, README.md, Jenkinsfile'
            sh 'ls -lah'
          }
        }
    }
}