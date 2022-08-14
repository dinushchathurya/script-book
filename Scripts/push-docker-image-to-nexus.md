### Push Docker Image to Nexus Private Docker repository

```
pipeline {

    agent { label 'Slave' }
    
    environment {
        imageName = "myapp"
        registryCredentials = "nexus"
        registry = "ec2-<server-ip>.ap-southeast-1.compute.amazonaws.com:8085/"
        dockerImage = ''
    }
    
    stages {

        // Checkout code from git repository
        stage('Code checkout') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/master']], 
                    extensions: [], 
                    userRemoteConfigs: [[url: 'https://github.com/dinushchathurya/html-nginx-docker.git']]
                ])
            }
        }
        
        // Build Docker image
        stage('Building image') {
          steps{
            script {
              dockerImage = docker.build imageName
            }
          }
        }
        
        // Uploading Docker images into Nexus Registry
        stage('Uploading to Nexus') {
         steps{  
             script {
                 docker.withRegistry( 'http://'+registry, registryCredentials ) {
                 dockerImage.push('latest')
              }
            }
          }
        }
    }
}
```