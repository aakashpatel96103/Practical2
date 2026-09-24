pipeline {
    agent any
 
    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository'
                git 'https://github.com/username/CalculatorApp.git'
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
