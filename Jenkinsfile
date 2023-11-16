pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Récupérer le code depuis le système de contrôle de version (par exemple, Git)
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Compiler le code Java
                sh 'javac -sourcepath src -d build app.java'
            }
        }

        stage('Test') {
            steps {
                // Exécuter les tests (par exemple, avec JUnit)
                sh 'java -cp build org.junit.runner.JUnitCore VotreClasseDeTest'
            }
        }

        stage('Email Notification') {
            steps {
                // Configurer les notifications par e-mail en cas d'échec
                emailext subject: 'Échec du pipeline Jenkins',
                          body: 'Il y a eu un échec dans le pipeline Jenkins. Veuillez vérifier et résoudre le problème.',
                          to: 'votre@email.com',
                          attachLog: true
            }
        }
    }

    post {
        // Actions à effectuer après l'exécution du pipeline
        failure {
            // Envoyer une notification en cas d'échec
            echo 'Le pipeline a échoué. Veuillez vérifier et résoudre le problème.'
        }
    }
}
