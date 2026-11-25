
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Obteniendo codigo del repositorio...'
                checkout scm
            }
        }

        stage('Test') {
            steps {
                echo 'Preparando entorno de pruebas...'

                sh '''
                    python3 -m venv .venv
                    .venv/bin/python -m pip install --upgrade pip
                    .venv/bin/python -m pip install -r api/requirements.txt
                '''

                echo 'Ejecutando pruebas automatizadas...'

                sh '''
                    cd api
                    ../.venv/bin/python -m pytest -v
                '''
            }
        }

        stage('Build') {
            steps {
                echo 'Generando archivo de configuracion...'

                sh '''
                    cp .env.example .env
                '''

                echo 'Construyendo imagenes de TaskFlow...'

                sh 'docker compose build'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Desplegando servicios de TaskFlow...'

                sh 'docker compose up -d'

                echo 'Verificando servicios desplegados...'

                sh 'docker compose ps'
            }
        }
    }
}
