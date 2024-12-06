pipeline {
    agent any

    stages {
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