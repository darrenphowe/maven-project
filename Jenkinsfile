pipeline{
    agent any
    stages{
        stage('Build'){
            steps{
                withMaven(jdk: 'JDK1.8', maven: 'Maven3.6') {
                    sh 'mvn clean package'
                }
            }
            post{
                success{
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy to Staging'){
            steps{
                build job: 'Deploy-to-staging'
            }
        }
    }
}