pipeline {
    agent any
    environment {
        MAIN_VERSION = "1.1"
        BUILD_VERSION = "${MAIN_VERSION}-b${env.BUILD_NUMBER}"
    }
    stages {
        stage('Clean') {
            steps {
                withMaven(maven: 'Maven 3.6.3') {
                    sh "mvn clean install -Dproduct.build.number=b${env.BUILD_NUMBER}"
                }
            }
        }
        stage('Compile') {
            steps {
                withMaven(maven: 'Maven 3.6.3') {
                    sh 'mvn compile'
                }
            }
        }
        stage('Test Junit & Mockito') {
            steps {
                withMaven(maven: 'Maven 3.6.3') {
                    sh 'mvn test'
                }
            }
        }
        stage('SonarQube analysis') {
            steps {
                withMaven(maven: 'Maven 3.6.3') {
                    sh '''
                    mvn sonar:sonar \
                        -Dsonar.projectKey=timesheet-devops \
                        -Dsonar.host.url=http://192.168.56.2:9000 \
                        -Dsonar.login=110b5a8288a0aee98ec5dcd225b0a3fc3b0f8441
                    '''
                }
            }
        }
        stage('Deploy to nexus') {
            steps {
                withMaven(maven: 'Maven 3.6.3') {
                    echo 'Deploying to nexus server'
                    sh 'mvn deploy'
                }
            }
        }
    }
}
