pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'javac -sourcepath src -d build App.java'
            }
        }

        stage('Test') {
            steps {
                script {
                    def compileResult = sh(script: 'javac -sourcepath src -d build App.java', returnStatus: true)
                    
                    if (compileResult != 0) {
                        error 'La compilation a échoué. Veuillez vérifier les erreurs de compilation.'
                    }
                }
            }
        }

    stage('post') {
        failure {
            script {
                emailext subject: 'Échec du pipeline Jenkins',
                          body: 'Il y a eu un échec dans le pipeline Jenkins. Veuillez vérifier et résoudre le problème.',
                          to: 'hamzaalibi95@gmail.com',
                          attachLog: true
            }
        }
    }
}
}
