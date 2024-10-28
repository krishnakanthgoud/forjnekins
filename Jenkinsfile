pipeline {
    agent any  

    tools {
        maven 'Maven_3.8.1'  
        jdk 'JDK11'          
    }

     stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/spring-projects/spring-petclinic.git'
            }
        }
        stage('Build') {
            steps {
                sh "mvn clean install"
            }
        }
        stage('sonarqube') {
            steps {
                sh "mvn clean install"
            }
        }

         stage('Test') {
            steps {
                sh 'mvn test'
            }

            post {
                always {
                    junit '**/target/surefire-reports/*.xml'  // Collect test results
                }
            }
        }
         stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
        