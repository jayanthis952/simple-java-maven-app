pipeline {
    agent any

    tools {
        maven 'Maven3'   // must match the name in Jenkins Global Tool Config
        jdk 'JDK17'      // use JDK17 instead of JDK11
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/jayanthis952/simple-java-maven-app.git'
            }
        }

        stage('Build') {
            steps {
                sh './mvnw clean package -B'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh './mvnw sonar:sonar -B'
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
