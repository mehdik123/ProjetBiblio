pipeline {
    agent any
    tools {
            jdk 'JDK21'
            maven 'MAVEN'
    }
    environment {
            REPO_URL = 'https://github.com/mehdik123/ProjetBiblio.git'
            SONARQUBE_CREDENTIALS_ID = 'sonar'
    }
    stages {
         stage('clean work-space') {
                    steps {
                        cleanWs()
                    }
         }
         stage('Checkout from github') {
                     steps {
                         git branch: 'main',
                         credentialsId: 'github',
                         url: REPO_URL
                     }
         }
        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Quality Analysis') {
            steps {
                withSonarQubeEnv(installationName: 'sonar' , credentialsId: SONARQUBE_CREDENTIALS_ID) {
                                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Déploiement simulé réussi'
            }
        }
    }
     post {
            success {
                mail(
                    to: 'mehdikamal535@gmail.com',
                    subject: 'Build Success',
                    body: 'Le build a été complété avec succès.'
                )
            }
            failure {
                mail(
                    to: 'mehdikamal535@gmail.com',
                    subject: 'Build Failed',
                    body: 'Le build a échoué.'
                )
            }
     }
}
