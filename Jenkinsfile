pipeline {
    agent any

    tools {
        maven "Maven"
    }

    stages {
        stage("Git Clone") {
            steps {
                git 'https://github.com/gitgo23/maven-web-app.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh "mvn clean package"
            }
        }

       stage('SonarQube Analysis') {
            environment {
                ScannerHome = tool 'Scanner-5'
            }
            steps {
                script {
                    withSonarQubeEnv('sonarqube') {
                        sh "${ScannerHome}/bin/sonar-scanner -Dsonar.projectKey=EcommerceApp -Dsonar.java.binaries=target/EcommerceApp/WEB-INF/classes"
                    }
                }
            }
        }

    
    }
}
