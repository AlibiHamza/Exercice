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
    }

    post {
        failure {
            script {
                try {
                    emailext subject: 'Échec du pipeline Jenkins',
                              body: 'Il y a eu un échec dans le pipeline Jenkins. Veuillez vérifier et résoudre le problème.',
                              to: 'hamzaalibi95@gmail.com',
                              attachLog: true
                } catch (Exception e) {
                    echo "Erreur lors de l'envoi de l'e-mail : ${e.message}"
                    e.printStackTrace()
                }
            }
        }
    }
}
