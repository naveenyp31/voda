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
        stage('Quality Gate status check'){
            steps{
                withSonarQubeEnv('sonar7.6'){
                sh 'mvn sonar:sonar'
                }
            }
        }
        stage('upload war file to nexus')
    }
}
