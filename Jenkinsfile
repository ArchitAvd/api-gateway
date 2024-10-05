pipeline{
    agent any
    tools{
        maven 'my-maven'
        jdk 'my-jdk'
    }
    stages{
        stage('Clone'){
            steps{
                git url:'https://github.com/ArchitAvd/api-gateway',branch:'master'
            }
        }
        stage('Build'){
            steps{
                bat "mvn clean install -DskipTests"
            }
        }
        stage('Test'){
            steps{
                bat "mvn test"
            }
        }
        stage('Deploy'){
            steps{
                bat "docker rm -f my-apig-container"
                bat "docker rmi -f my-apig-image"
                bat "docker build -t my-apig-image ."
                bat "docker run -p 8060:8060 -d --name my-apig-container my-apig-image"
            }
        }
    }
}