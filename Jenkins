pipeline {
    agent any

    stages {
        stage('Install HTTP Server') {
            steps {
                script {
                    // Встановлення HTTP-сервера (приклад для Apache)
                    sh 'sudo apt-get update'
                    sh 'sudo apt-get install apache2'
                }
            }
        }

        stage('Check 4xx and 5xx Errors') {
            steps {
                script {
                    // Аналіз лог-файлу та перевірка на помилки 4xx та 5xx
                    def logErrors = sh(script: "sudo grep ' 4[0-9]\\{2\\}\\| 5[0-9]\\{2\\}' /var/log/apache2/access.log", returnStatus: true)

                    if (logErrors == 0) {
                        echo "No 4xx or 5xx errors found in logs."
                    } else {
                        echo "Found 4xx or 5xx errors in logs."
                        currentBuild.result = 'UNSTABLE'
                        
                    }
                }
            }
        }
    }

}
