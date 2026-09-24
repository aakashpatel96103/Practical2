pipeline {
    agent any

    environment {
        PATH = "C:\\Program Files\\Java\\jdk-21.0.12\\bin;${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/aakashpatel96103/Practical2.git'
            }
        }

        stage('Build') {
            steps {
                bat 'javac src\\*.java'
                bat 'jar cfm CalculatorApp.jar manifest.txt -C src .'
            }
        }
    }
}
