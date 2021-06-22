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
        stage('Quality Gate status check'){
            steps{
                withSonarQubeEnv('sonar7.6'){
                sh 'mvn sonar:sonar'
                }
                timeout(time: 1, unit: 'HOURS') {
                   def qg = waitforQualityGate()
                   if (qg.status != 'ok'){
                       error "pipeline aborted due to Quality gate failure: ${qg.status}"
                    }  
                }
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