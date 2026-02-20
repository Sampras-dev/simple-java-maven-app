pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    environment {
        SONAR_PROJECT_KEY = "java"
    }


    stages{
        stage('checkout') {
            steps {
                git 'https://github.com/Sampras-dev/simple-java-maven-app.git'


            }
        }

        stage('Build and compile') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('unit Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Sonarqube analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh """ 
                    mvn sonar:sonar \
                    -Dsonar.projectkey=${SONAR_PROJECT_KEY}
                    
                    """
                }
             }
        }

    }



    post {
        success { 
            echo 'Build and sonarQube scan successfull'
        }
        failure {
            echo 'Build failed and retry'
        }
    }
}
