pipeline {
    agent { label 'Jenkins-Agent' }

    tools {
        jdk 'Java17'
        maven 'Maven3'
    }

    environment {
        SONAR_HOST_URL = 'http://<your-sonarqube-ip>:9000'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/sreeja-17-lab/register-app'
            }
        }

        stage('Build') {
            steps {
                dir('register-app') {
                    sh 'mvn clean package'
                }
            }
        }

        stage('Test') {
            steps {
                dir('register-app') {
                    sh 'mvn test'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                dir('register-app') {
                    withSonarQubeEnv('jenkins-sonarq-token') {
                        sh "mvn sonar:sonar -Dsonar.projectKey=register-app -Dsonar.host.url=$SONAR_HOST_URL"
                    }
                }
            }
        }
    }
}
