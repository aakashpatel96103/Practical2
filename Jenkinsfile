pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git  branch: 'main',
                url:'https://github.com/aakashpatel96103/Practical2.git'
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
