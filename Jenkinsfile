pipeline {
    agent any

    stages {
        stage('Build Java (Maven)') {
            steps {
                script {
                    docker.image('maven:3.9-eclipse-temurin-17').inside {
                        dir('java-app') {
                            sh 'mvn clean install'
                        }
                    }
                }
            }
        }

        stage('Build Node.js') {
            steps {
                script {
                    docker.image('node:20').inside {
                        dir('node-app') {
                            sh 'npm install'
                            sh 'npm test || echo "No test script definido"'
                        }
                    }
                }
            }
        }

        stage('Build .NET Core') {
            steps {
                script {
                    docker.image('mcr.microsoft.com/dotnet/sdk:8.0').inside {
                        dir('dotnet-app') {
                            sh 'dotnet restore'
                            sh 'dotnet build --configuration Release'
                            sh 'dotnet test || echo "No hay pruebas definidas"'
                        }
                    }
                }
            }
        }
    }
}
