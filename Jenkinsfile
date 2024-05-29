pipeline {
    agent any
    tools{
        jdk 'jdk17'
        maven 'maven3'
    }

    stages {
        stage('git-checkout') {
            steps {
                git 'https://github.com/sajal55/new-test.git'
            }
        }

        stage('Code-Compile') {
            steps {
               sh "mvn clean compile"
            }
        }
        
        stage('Unit Tests') {
            steps {
               sh "mvn test"
            }
        }
		 
        stage('Code-Build') {
            steps {
               sh "mvn clean package"
            }
        }

         stage('Docker Build') {
            steps {
               script{
                   withDockerRegistry(credentialsId: 'docker-cred') {
                    sh "docker build -t  santa123 . "
                 }
               }
            }
        }

        stage('Docker Push') {
            steps {
               script{
                   withDockerRegistry(credentialsId: 'docker-cred') {
                    sh "docker tag santa123 sajalsharma125/new-secret:latest"
                    sh "docker push sajalsharma125/new-secret:latest"
                 }
               }
            }
        }
        
        	 
        stage('Docker Image Scan') {
            steps {
               sh "trivy image adijaiswal/santa123:latest "
            }
        }}    
}
