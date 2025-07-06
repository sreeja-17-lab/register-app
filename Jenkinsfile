pipeline {
    agent {
        label 'Jenkins-Agent' // Replace with your agent label, if different
    }

    tools {
        jdk 'Java17'         // Make sure this matches the name under Global Tool Configuration
        maven 'Maven3'       // Same here
    }

    environment {
        SONAR_HOST_URL = 'http://<your-sonarqube-ip>:9000'  // 🔁 Replace with actual SonarQube IP or domain
    }

    stages {
        stage('Checkout from SCM') {
            steps {
                git branch: 'main',
                    credentialsId: 'github',
                    url: 'https://github.com/sreeja-17-lab/register-app'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('jenkins-sonarq-token') {
                    sh "mvn sonar:sonar -Dsonar.projectKey=register-app -Dsonar.host.url=$SONAR_HOST_URL"
                }
            }
        }
    }
}
