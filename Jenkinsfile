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
    }
}