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
                build job: 'deploy-to-staging'
            }
        }
        stage('Deploy to Production'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?', submitter: darrenphowe
                }
                build job: 'deploy-to-production'
            }
            post{
                success{
                    echo 'Code deployed to Production.'
                }
                failure{
                    echo 'Deployment failed.'
                }
            }
        }
    }
}