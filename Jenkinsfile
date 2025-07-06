pipeline {
    agent any

    tools {
        jdk 'Java17'
        maven 'Maven3'
    }

    stages {
        stage('Checkout Code') {
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
                        sh "mvn sonar:sonar -Dsonar.projectKey=register-app -Dsonar.host.url=http://<your-sonarqube-ip>:9000"
                    }
                }
            }
        }
    }
}
