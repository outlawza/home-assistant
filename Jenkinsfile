pipeline {
    agent any
    stages{
        stage('Init'){
            steps {
                echo 'Testing...'
            }
        }

        stage('Build'){
            steps {
                echo 'Biilding...'
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deploy to Staging'){
            steps {
                echo 'Code Deployed. Hooraa!!!'
                build job: 'deploy-to-staging'
            }
        }
        stage ('Deploy to Prod'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve Production Deployment?'
                }
                build job: 'Deploy-to_prod'
            }
            post {
                success {
                    echo 'Code deployed to production....'
                }
                failure {
                    echo 'Deployment failed. O no....'
                }
            }
        }
    }
}