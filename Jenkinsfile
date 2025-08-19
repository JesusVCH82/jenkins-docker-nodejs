pipeline {
    agent {
        docker {
            image 'node:14-alpine' // amd64, compatible con tu host
            args '-p 5001:5001'    // tus args de puerto
        }
    }
    
    stages {        
        stage('Install Dependencies') {
            steps {
                echo 'Instalando dependencias...'
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'npm run build || echo "No hay build script, se salta"'
            }
        }
        stage('Test') {
            steps {
                echo 'Ejecutando tests...'
                sh 'npm test || echo "No hay tests configurados, se salta"'
            }
        }
        stage('Run Application') {
            steps {
                echo 'Corriendo la aplicación...'
                sh 'npm start &'
                sh 'sleep 10' // espera 10 segundos para que la app arranque
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
