pipeline {
    agent any

    environment {
      NAME_FOLDER_ZIP = "source.zip"
      WORKSPACE = "${env.WORKSPACE}"
      HOST_SFTP = "ftp.concafras.com"
    }

    stages {
      // stage("Build") {
      //   steps {
      //     echo "..:: INÍCIO DO BUILD ::.."

      //     echo ".: Empacontando arquivos em ${NAME_FOLDER_ZIP} :."
      //     // zip zipFile: NAME_FOLDER_ZIP,
      //     //     archive: false,
      //     //     exclude: '.git, .editorconfig, README.md, Jenkinsfile',
      //     //     overwrite: true
      //   }
      // }
      stage("Build & Deploy") {
        steps {
          echo "..:: INÍCIO BUILD ::.."
          script {
            def files = findFiles(glob: 'index.html, favicon.ico, pages/**, assets/**')

            echo "${files}"

            echo "..:: INÍCIO DEPLOY ::.."

            dir("alegria-scripts") {
              // Realiza o clone
              git branch: 'main',
                  credentialsId: 'GitHub_Username',
                  url: 'https://github.com/viniciusks/alegria-scripts.git'

              withCredentials([usernamePassword(credentialsId: 'user_sftp_concafras', passwordVariable: 'passSftp', usernameVariable: 'userSftp')]) {
                withPythonEnv("/usr/bin/python3") {
                  sh "pip3 install -r requirements.txt"
                  files.each { file ->
                    echo "${file}"
                    if(file == "index.html") {
                      echo "${file}"
                      sh "python3 send_sftp.py ${HOST_SFTP} ${userSftp} ${passSftp} ${file}"
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
    post {
      always {
        echo "..:: Limpando workspace ::.."
        cleanWs()
      }
    }
}