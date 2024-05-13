pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Fetch the code from the master branch of GitHub
                git branch: 'master', url: 'https://github.com/Slimdrissi123/timesheet-devops.git'
            }
        }
        
        stage('Clean') {
            steps {
                // Clean the Maven project
                sh 'mvn clean install'
            }
        }
        
        stage('Compile') {
            steps {
                // Compile the Maven project
                sh 'mvn compile'
            }
        }
        
        stage('Test Junit & Mockito'){
            steps{
                sh 'mvn test'
            }
        }
        
        stage('SonarQube analysis') {
            steps {
                // Exécution de l'analyse de code avec SonarQube
                withSonarQubeEnv('SonarQube') {
                      sh 'mvn sonar:sonar \
                          -Dsonar.projectKey=timesheet-devops \
                          -Dsonar.host.url=http://192.168.56.2:9000 \
                          -Dsonar.login=110b5a8288a0aee98ec5dcd225b0a3fc3b0f8441'
                }
            }
        }
        
    }
}
