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
                sh 'javac -sourcepath src -d build App.java'
            }
        }

    stage('Test') {
    steps {
        script {
            // Utiliser JUnit pour exécuter les tests
            def junitResults = sh(script: 'java -cp build org.junit.runner.JUnitCore App.java', returnStatus: true)
            
            // Vérifier si les tests ont réussi
            if (junitResults != 0) {
                error 'Les tests ont échoué. Veuillez vérifier les résultats.'
            }
        }
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
