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
                    jq --version
                '''
            }
        }
        stage("Prune Docker Data") {
            steps {
                bat 'docker system prune -a --volume -f'
            }
        }
        stage("Start Container") {
            steps {
                bat 'docker-compose up -d --no-color --wait'
                bat 'docker compose ps'
            }
        }
    }
}