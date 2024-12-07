pipeline {
    agent any
    environment {
        ANSIBLE_HOST_KEY_CHECKING = "False"
    }

    stages {
        stage('ls') {
            steps {
                script {
                    sh 'ls'
                }
            }
        }

        stage('Install Ansible') {
            steps {
                echo 'Installing Ansible...'

                sh '''
                  if ! [ -x "$(command -v ansible)" ]; then
                    if [ "$(uname)" == "Darwin" ]; then
                      brew install ansible
                    else
                      sudo apt update
                      sudo apt install -y ansible
                    fi
                  fi
                '''
            }
        }

        stage('Подготовка окружения') {
            steps {
                script {
                    ansiblePlaybook playbook: 'prepare-environment.yml'
                }
            }
        }
        stage('Запуск приложений') {
            steps {
                script {
                    ansiblePlaybook playbook: 'start_application.yml'
                }
            }
        }
    }
}