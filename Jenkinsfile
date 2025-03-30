pipeline {
    agent any
    stages {
        stage("verifying tooling") {
            steps {
                bat '''
                    docker version
                    docker info
                    docker compose version
                    curl --version
                '''
            }
        }
        stage("Prune Docker Data") {
            steps {
                bat 'docker system prune -a --volumes -f'
            }
        }
        stage("Start Container") {
            steps {
                bat 'docker compose up -d --no-color --wait'
                bat 'docker compose ps'
            }
        }
        stage("Check Response"){
            steps {
                bat 'curl http://localhost'
            }
        }
    }
    post {
        always {
            bat 'docker compose down --remove-orphans -v'
            bat 'docker compose ps'
        }
    }
}
