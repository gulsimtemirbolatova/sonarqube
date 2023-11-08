pipeline {
    agent any

    environment {
        SONARQUBE_HOSTNAME = 'sonarqube'
    }

    tools {
        gradle 'gradle-4.10.2'
        sonar 'sonar'
    }

    stages {
        stage('prep') {
            steps {
                git 'https://github.com/cloudacademy/devops-webapp.git'
            }
        }

        stage('build') {
            steps {
                script {
                    sh 'gradle build'
                }
            }
        }

        stage('sonar-scanner') {
            steps {
                withCredentials([string(credentialsId: 'sonar', variable: 'sonarLogin')]) {
                    script {
                        sh "sonar-scanner -e -Dsonar.host.url=http://${env.SONARQUBE_HOSTNAME}:9000 -Dsonar.login=${sonarLogin} -Dsonar.projectName=WebApp"
                    }
                }
            }
        }
    }
}

