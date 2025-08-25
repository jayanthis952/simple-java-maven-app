pipeline {
    agent any

    tools {
        maven 'Maven3'   // Must match Jenkins Maven global config
        jdk 'JDK21'      // Must match Jenkins JDK global config
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/jayanthis952/simple-java-maven-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -B'
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed. Please check the logs.'
        }
    }
}
