def nameFolderZip = "source.zip"

pipeline {
    agent any

    stages {
        stage('Build') {
          steps {
            cleanWs()
            echo 'Começou o build...'
            zip zipFile: nameFolderZip,
                archive: false,
                exclude: '.git .editorconfig README.md Jenkinsfile'
            sh 'ls -lah'
            sh "mkdir dist && cp ${nameFolderZip} dist"
            unzip zipFile: "dist/${nameFolderZip}"
            sh 'ls -lah dist/'
          }
        }
    }
}