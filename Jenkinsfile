pipeline {
    agent none
    //     environment {
    //     ENV_DOCKER = credentials('dockerhub')
    //     SONAR_TOKEN = credentials('sonar')
    //     DOCKERIMAGE = "full-stack-app-demo"
    //     EKS_CLUSTER_NAME = "demo-cluster"
    // }
    stages {
        stage('Build') {
            agent {
                docker { 
                    image 'maven:3.8.1-adoptopenjdk-11' 
                    args '-v /root/.m2:/root/.m2' 
                }
            }
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('SonarQube') {
            agent {
                docker { image 'sonarsource/sonar-scanner-cli:latest' }
            }
            steps {
                echo 'Sonaqube step'
                sh 'sonar-scanner'
            }
        }
    }
}
