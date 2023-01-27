pipeline {
    agent any

    environment {
      NAME_FOLDER_ZIP = "source.zip"
      ABSOLUTE_PATH_ZIP = "${env.WORKSPACE}/${NAME_FOLDER_ZIP}"
      HOST_SFTP = "ftp.concafras.com"
    }

    stages {
        stage("Build") {
          steps {
            echo "..:: INÍCIO DO BUILD ::.."

            echo ".: Empacontando arquivos em ${NAME_FOLDER_ZIP} :."
            zip zipFile: NAME_FOLDER_ZIP,
                archive: false,
                exclude: '.git, .editorconfig, README.md, Jenkinsfile',
                overwrite: true
          }
        }
        stage("Deploy") {
          steps {
            echo "..:: INÍCIO DEPLOY ::.."

            // Realiza o clone
            git branch: 'main',
                credentialsId: 'GitHub_Username',
                url: 'https://github.com/viniciusks/alegria-scripts.git'

            dir("alegria-scripts") {
              withCredentials([usernamePassword(credentialsId: 'user_sftp_concafras', passwordVariable: 'passSftp', usernameVariable: 'userSftp')]) {
                withPythonEnv("/usr/bin/python3") {
                  sh "pip3 install -r requirements.txt"
                  sh "python3 send_sftp.py ${HOST_SFTP} ${userSftp} ${passSftp} ${ABSOLUTE_PATH_ZIP}"
                }
              }
            }
          }
        }
    }
}