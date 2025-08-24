pipeline {
    agent any

    tools {
        maven 'Maven3'   // Must match the Maven installation name in Jenkins
        jdk 'JDK17'      // Must match the JDK installation name in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/jayanthis952/simple-java-maven-app.git'
            }
        }

        stage('Build') {
            steps {
                // Use global Maven, not mvnw
                sh 'mvn clean package -B'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar -B'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
