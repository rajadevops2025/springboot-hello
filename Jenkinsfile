pipeline {
    agent any 
    tools {
        maven 'maven3'    
    }
    stages {
        stage('Compile and Clean') { 
            steps {
                // Run Maven on a Unix agent.
              
                bat "mvn clean compile"
            }
        }
        stage('deploy') { 
            
            steps {
                bat "mvn package"
            }
        }
        stage('Build Docker image'){
          
            steps {
                echo "Hello Java Express"
                bat 'dir'
                bat 'docker build -t rajadevops2025/docker_jenkins_springboot:%BUILD_NUMBER% .'
            }
        }
        stage('Docker Login'){
            
            steps {
                 withCredentials([string(credentialsId: 'DockerId', variable: 'Dockerpwd')]) {
                    bat "docker login -u rajadevops2025 -p %Dockerpwd%"
                }
            }                
        }
        stage('Docker Push'){
            steps {
                bat 'docker push rajadevops2025/docker_jenkins_springboot:%BUILD_NUMBER%'
            }
        }
        stage('Docker deploy'){
            steps {
                bat 'docker run -itd -p 8081:9090 rajadevops2025/docker_jenkins_springboot:%BUILD_NUMBER%'
            }
        }
        stage('Archving') { 
            steps {
                 archiveArtifacts '**/target/*.jar'
            }
        }
    }
}

