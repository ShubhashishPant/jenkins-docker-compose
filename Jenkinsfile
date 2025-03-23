pipeline {
    agent any
    stages {
        stage("verifying tooling") {
            steps {
                sh '''
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
                sh 'docker system prune -a --volume -f'
            }
        }
        stage("Start Container") {
            steps {
                sh 'docker-compose up -d --no-color --wait'
                sh 'docker compose ps'
            }
        }
    }
}