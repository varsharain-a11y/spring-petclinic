pipeline {
    agent any 
    tools {
        maven '3.9.0'
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
                    docker.withRegistry('https://a0cd8nopnuden.jfrog.io/artifactory/test/', 'test/') {
                        docker.image("petclinic:${env.BUILD_NUMBER}").push()
                    }
                }
            }
        }
    }
}
