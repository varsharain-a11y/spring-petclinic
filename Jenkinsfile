pipeline {
    agent any
    tools {
        maven 'Maven 3.8.6'
        jdk 'Java 17.0.4.1'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("petclinic:${env.BUILD_NUMBER}")
                }
            }
        }
        stage('Push Docker Image to Registry') {
            steps {
                script {
                    docker.withRegistry('https://frog-artifactory.com', 'frog-registry') {
                        docker.image("petclinic:${env.BUILD_NUMBER}").push()
                    }
                }
            }
        }
    }
}
