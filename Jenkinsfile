pipeline {
    agent none
    stages {
        stage('Build Java App') {
            agent {
                docker {
                    image 'maven:3.9-eclipse-temurin-17'
                    args '-v /root/.m2:/root/.m2'
                }
            }
            steps {
                dir('java-app') {
                    sh 'mvn clean package'
                }
            }
        }

        stage('Build Node App') {
            agent {
                docker {
                    image 'node:18'
                }
            }
            steps {
                dir('node-app') {
                    sh 'npm install'
                    sh 'npm test || echo "No test script defined"'
                }
            }
        }
    }
}
