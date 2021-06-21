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
        stage('deploy into tomcat server'){
            steps{
                sshagent(['tomcat9']) {
                 sh """
                 scp -o StrictHostKeyChecking=no target/*.war ec2-user@10.0.0.239:/opt/apache-tomcat-9.0.46/webapps/
                 ssh /opt/apache-tomcat-9.0.46/bin/shutdown.sh
                 ssh /opt/apache-tomcat-9.0.46/bin/startup.sh
                 """
                }
            }
        }
    }
}