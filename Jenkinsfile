pipeline{
    agent any
    tools {
        maven 'maven381'
    }
    stages{
        stage('checkout'){
            steps{
                git credentialsId: 'Git_cred', 
                url: 'https://github.com/naveenyp31/voda.git'
            }
        }
        stage('Build'){
            steps{
                sh 'mvn clean install -DskipTests'
            }
        }
        stage('tests'){
            steps{
                sh 'mvn test'
            }
        }
    }
}