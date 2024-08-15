pipeline {
    agent any

    stages {
        stage('Checkout code') {
            //checkout the repository
            steps {
                git branch: 'main', url: 'https://github.com/Pain1003/JenkinsSeleniumWebDriver_Demo_8_16'
            }
        }
        stage('Set up .Net Core') {
            //install dot net
            steps {
                bat '''
                Echo Downloading .Net 6 SDK
                curl -l -o dotnet-sdk-6.0.133-win-x86.exe https://download.visualstudio.microsoft.com/download/pr/0b870df1-1fae-489f-a035-2cbd41726cd4/d44c685cd37ac022c12eab695d14694b/dotnet-sdk-6.0.133-win-x86.exe
                echo Installing dotnet-sdk-6.0.133-win-x86.exe
                dotnet-sdk-6.0.133-win-x86 /quiet /norestart
                '''
            }
        }
        stage('Restore dependencies') {
            //install dependencies
            steps {
                bat 'dotnet restore SeleniumBasicExercise.sln'
            }
        }
        stage('Build') {
            //build
            steps {
                bat 'dotnet build SeleniumBasicExercise.sln --configuration Release'
            }
        }
        stage('Run Tests TestProject1') {
            //run tests
            steps {
                bat 'dotnet test TestProject1/TestProject1.csproj --logger "trx;LogFileName=TestResults.trx"'
            }
        }

        stage('Run Tests TestProject2') {
            //run tests
            steps {
                bat 'dotnet test TestProject2/TestProject2.csproj --logger "trx;LogFileName=TestResults.trx"'
            }
        }

        stage('Run Tests TestProject3') {
            //run tests
            steps {
                bat 'dotnet test TestProject3/TestProject3.csproj --logger "trx;LogFileName=TestResults.trx"'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: true
            step ([
                $class: 'MSTestPublisher',
                TestResultsFile: '**/TestResults/*.trx'
            ])
        }
    }
}