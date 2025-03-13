pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                sh 'dotnet restore' 
                sh 'dotnet build --no-restore' 
            }
        }
        stage('Test') { 
            steps {
                sh 'dotnet test --no-build --no-restore --collect "XPlat Code Coverage"' 
            }
            post {
                always {
                    junit 'SimpleWebApi.Test/TestResults/**/*.xml' 
                }
            }
        }
        stage('Deliver') { 
            steps {
                sh 'dotnet publish --no-build --no-restore -o published' 
            }
            post {
                success {
                    archiveArtifacts 'published'
                }
            }
        }
    }
}