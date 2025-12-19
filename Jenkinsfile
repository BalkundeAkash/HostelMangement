pipeline {
    agent any

    tools {
        maven 'Maven-3.9.11'
        jdk 'JDK-17'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Run Application') {
            steps {
                sh '''
                echo "Stopping old app (if running)..."
                pkill -f hostelmanagement || true

                echo "Starting Spring Boot app..."
                nohup java -jar target/*.jar > app.log 2>&1 &

                sleep 10
                '''
            }
        }

        stage('App Info') {
            steps {
                echo '===================================='
                echo 'Spring Boot App is running!'
                echo 'URL: http://localhost:8080/hello'
                echo '===================================='
            }
        }
    }
}
