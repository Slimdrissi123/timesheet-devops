MAIN_VERSION = "1.0"
BUILD_VERSION = "$MAIN_VERSION-b${env.BUILD_NUMBER}"
BUILD_INFO = maven.newBuildInfo()
pipeline {
    agent any
    stages {
        
        
        stage('Clean') {
            steps {
                sh "mvn clean install -Dproduct.build.number=b$env.BUILD_NUMBER".toString()
            }
        }
        
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
        
       stage('Test Junit & Mockito'){
            steps{
                sh 'mvn test'
            }
        }
        
        stage('SonarQube analysis') {
            steps 
                 {
                      sh 'mvn sonar:sonar \
                          -Dsonar.projectKey=timesheet-devops \
                          -Dsonar.host.url=http://192.168.56.2:9000 \
                          -Dsonar.login=110b5a8288a0aee98ec5dcd225b0a3fc3b0f8441'
                }
            
        }
        stage('Deploy to nexus'){
            steps
                {
                    echo 'Deploying to nexus server'
                    sh 'mvn deploy'
                }
        }

        
    }
}
