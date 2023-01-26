pipeline {
    agent any

    environment {
      NAME_FOLDER_ZIP = "source.zip"
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

            dir("devops") {
              withPythonEnv("/usr/bin/python3") {
                sh "python3 send_sftp.py"
              }
            }
          }
        }
    }
}