def nameFolderZip = "source.zip"

pipeline {
    agent any

    stages {
        stage('Build') {
          steps {
            echo 'Começou o build...'
            zip zipFile: nameFolderZip,
                archive: false,
                exclude: '.git, .editorconfig, README.md, Jenkinsfile'
            sh 'ls -lah'
            sh "mkdir dist && mv ${nameFolderZip} dist"
            unzip zipFile: "dist/${nameFolderZip}",
                  dir: "dist"
            sh 'ls -lah dist/'
            sh 'rm -rf dist'
          }
        }
    }
}