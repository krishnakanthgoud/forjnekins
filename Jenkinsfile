pipeline {
    agent any  

    tools {
        maven 'MVN_3.9'  
        jdk 'JDK_17'          
    }

     stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/krishnakanthgoud/forjnekins.git'
            }
        }
        stage('Build') {
            steps {
                sh "mvn clean install"
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SONAR') {  // Replace 'SonarQube' with your server name
                    sh """
                        mvn clean verify sonar:sonar \
                        -Dsonar.projectKey=SPRING \
                        -Dsonar.host.url=http://18.61.231.252:9000 \
                        -Dsonar.login=sqp_5057fa4c5f0bf3f07d7d76745a54f6545f0a7e74
                    """
                }
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
        

     }
}