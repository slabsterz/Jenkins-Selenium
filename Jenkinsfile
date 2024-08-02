pipeline {
    agent any

    stages {
        stage('Checkout code') {
            steps {
                git branch: 'main', url: 'https://github.com/slabsterz/Jenkins-Selenium'
            }
        }

        stage('Install SDK') {
            steps {
                bat '''
                echo Install .NET SDK 6
                curl -l -o dotnet-sdk-6.0.424-win-x64.exe https://download.visualstudio.microsoft.com/download/pr/23c7bf0d-e22d-4372-bcb2-292eb36a5238/11af494be409759f46b679ab22e65a58/dotnet-sdk-6.0.424-win-x64.exe
                echo Installing
                dotnet-sdk-6.0.424-win-x64.exe /quiet /norestart
                '''
            }
        }

        stage('Restoring NuGet') {
            steps {
                bat 'dotnet restore SeleniumIde.sln'
            }
        }

        stage('Building') {
            steps {
                bat 'dotnet build SeleniumIde.sln --configuration Release'
            }
        }

        stage('Run tests') {
            steps {
                bat 'dotnet test SeleniumIde.sln --logger "trx;LogFileName=TestResults.trx"'
            }
        }  
    }

    post {
        always {
            archiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: true
            step([
                $class: 'MSTestPublisher',
                testResultsFile: '**/TestResults/*.trx'
            ])
        }
    } 
}
