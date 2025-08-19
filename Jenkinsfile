pipeline {
    agent {
        docker {
            image 'arm64v8/node:14-alpine'
            args '--platform linux/arm64 -p 5001:5001'
        }
    }
    
    stages {        
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build') {
            steps {
                echo 'Building the application...'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Run Application') {
            steps {
                sh 'npm start &'
                sh 'sleep 60' // esperar que la app inicie
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
