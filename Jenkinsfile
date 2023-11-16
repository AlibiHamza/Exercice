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

        stage('Email Notification') {
            steps {
                script {
                  emailext (attachLog: true, body: 'Il y a eu un échec dans le pipeline Jenkins. Veuillez vérifier et résoudre le problème.', subject: 'Echec du pipeline Jenkins', to: 'hamzaalibi95@gmail.com')
                }
            }
        }
    }
}
