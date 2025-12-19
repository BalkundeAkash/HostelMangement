pipeline {
    agent any

    tools {
        jdk 'JDK21'
        maven 'Maven3'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                  echo "Stopping old application if running..."
                  pkill -f hostelmanagement || true

                  echo "Starting Spring Boot application..."
                  nohup java -jar target/*.jar > app.log 2>&1 &
                '''
            }
        }

        stage('Application Info') {
            steps {
                echo '----------------------------------------'
                echo 'Application deployed successfully 🚀'
                echo 'Open URL: http://localhost:8080/hello'
                echo '----------------------------------------'
            }
        }
    }
}
