pipeline {
    agent any
    tools {
        scannerHome 'sonarcloud'
    }
    stages {
        stage('vcs') {
            steps {
                git branch: 'dev',
                    url: 'https://github.com/dhille98/SampleWeb.git'
            }
        }
        stage('build and analysis') {
            steps {
                
                withSonarQubeEnv(credentialsId: 'SONAR_CLOUD', installationName: 'sonarcloud') {
                    sh 'dotnet sonarscanner begin /k:"app-123_sampleweb" '
                    sh 'dotnet build SampleMVC.sln --no-incremental'
                    sh 'dotnet test SampleMVC.sln'
                    sh 'dotnet publish -c Release StudentsWeb/StudentsWeb.csproj -o published/'
                    sh 'dotnet sonarscanner end'
                    
                }
                
            }
        }
    }
}

def scannerHome = tool 'SonarScanner for MSBuild'
    withSonarQubeEnv() {
      sh "dotnet ${scannerHome}/SonarScanner.MSBuild.dll begin /k:\"app-123\""
      sh "dotnet build"
      sh "dotnet ${scannerHome}/SonarScanner.MSBuild.dll end"


      withSonarQubeEnv(credentialsId: 'SONAR_CLOUD', installationName: 'sonarcloud') {
                    sh 'dotnet sonarscanner begin /k:"april24_sampleweb" /o:april24'
                    sh 'dotnet build SampleMVC.sln --no-incremental'
                    sh 'dotnet test SampleMVC.sln'
                    sh 'dotnet publish -c Release StudentsWeb/StudentsWeb.csproj -o published/'
                    sh 'dotnet sonarscanner end'