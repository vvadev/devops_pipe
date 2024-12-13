pipeline {
    agent any
    environment {
        ANSIBLE_HOST_KEY_CHECKING = "False"
    }

    stages {

        stage('Install Ansible') {
            steps {
                echo 'Installing Ansible...'

                sh '''
                  if ! [ -x "$(command -v ansible)" ]; then
                    if [ "$(uname)" == "Darwin" ]; then
                      brew install ansible
                    else
                      sudo apt install -y ansible
                    fi
                  fi
                '''
            }
        }

        stage('Подготовка окружения') {
            steps {
                script {
                    ansiblePlaybook( playbook: 'prepare-environment.yml', inventory: 'inventory' )
                }
            }
        }
        stage('Запуск приложений') {
            steps {
                script {
                    ansiblePlaybook( playbook: 'start_application.yml', inventory: 'inventory' )
                }
            }
        }
    }
}