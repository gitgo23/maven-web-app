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
    }
}
