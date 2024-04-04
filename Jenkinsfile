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
                        sh "${ScannerHome}/bin/sonar-scanner -Dsonar.projectKey=Maven-App"
                    }
                }
            }
        }

        stage('Deploy to Nexus') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: '01-maven-web-app', 
                classifier: '', 
                file: 'target/maven-web-app.war', 
                type: 'war']], 
                credentialsId: 'NEXUS_CRED', 
                groupId: 'in.ashokit', 
                nexusUrl: '54.234.72.14:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: 'ashokit', 
                version: '3.0-RELEASE'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'TOMCAT', 
                path: '', 
                url: 'http://54.87.204.112:8080/')], 
                contextPath: null, 
                war: 'target/*.war'
            }
        }

    
    }
}
