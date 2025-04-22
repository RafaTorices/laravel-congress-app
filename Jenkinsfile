pipeline {
    agent any

    environment {
        APP_ENV = 'testing'
        DB_CONNECTION = 'sqlite'
        DB_DATABASE = 'database/database.sqlite'
    }

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'github-token', url: 'https://github.com/RafaTorices/laravel-congress-app'
            }
        }

        stage('Composer install') {
            steps {
                sh 'composer install --no-interaction --prefer-dist --optimize-autoloader'
            }
        }

        stage('Crear archivo .env') {
            steps {
                sh 'cp .env.example .env'
                sh 'php artisan key:generate'
            }
        }

        stage('Migrar base de datos') {
            steps {
                sh 'touch database/database.sqlite'
                sh 'php artisan migrate --force'
            }
        }

        stage('Tests') {
            steps {
                sh 'php artisan test'
            }
        }
    }
}