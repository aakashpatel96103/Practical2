pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                // Universal SCM checkout: checks out current job's repository & branch on any system
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        // Linux / macOS agent
                        sh '''
                            javac src/*.java
                            jar cfm CalculatorApp.jar manifest.txt -C src .
                        '''
                    } else {
                        // Windows agent: dynamically resolves javac/jar without hardcoded machine paths
                        bat '''
                            @echo off
                            where javac >nul 2>&1
                            if %errorlevel% equ 0 goto :COMPILE

                            if defined JAVA_HOME (
                                if exist "%JAVA_HOME%\\bin\\javac.exe" (
                                    set "PATH=%JAVA_HOME%\\bin;%PATH%"
                                    goto :COMPILE
                                )
                            )

                            for /d %%D in ("%ProgramFiles%\\Java\\jdk*" "%ProgramFiles(x86)%\\Java\\jdk*" "%ProgramFiles%\\Eclipse Adoptium\\jdk*") do (
                                if exist "%%D\\bin\\javac.exe" (
                                    set "PATH=%%D\\bin;%PATH%"
                                    goto :COMPILE
                                )
                            )

                            :COMPILE
                            javac src\\*.java
                            jar cfm CalculatorApp.jar manifest.txt -C src .
                        '''
                    }
                }
            }
        }
    }
}
