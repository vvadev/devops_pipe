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
        stage('Подготовка окружения') {
            steps {
                script {
                    ansiblePlaybook playbook: 'DevOps/prepare-environment.yml'
                }
            }
        }
        stage('Запуск приложений') {
            steps {
                script {
                    ansiblePlaybook playbook: 'DevOps/start_application.yml'
                }
            }
        }
    }
}