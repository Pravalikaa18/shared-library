pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                sh 'pip install . && pytest'
            }
        }
        stage('Build Docker') {
            steps {
                sh 'docker build -t pravalikaa18/sharedlib:0.1.0 .'
            }
        }
        stage('Push Docker') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'Dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push pravalikaa18/sharedlib:0.1.0'
                }
            }
        }
    }
}
