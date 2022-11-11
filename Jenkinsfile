
pipeline {
    
    environment {
    imagename = "Ranga9346/spring-petclinics"
    registryCredential = 'mycredentials'
    dockerImage = ''
  }
    agent any

    stages {
        
        
        
        stage('git') {
            steps {
                echo 'clonning Repository'
                git branch: 'main', url: 'https://github.com/Ranga9346/spring-petclinic.git'
                
                echo 'Repo clone successfully'
            }
            
        }
        
        
       stage('BUILD') {
            steps {
                echo 'Build the code'
                sh './mvnw package'
            }
       }
            
            
            
            
            stage('DOCKERIZE') {
            steps {
                echo 'Deploy the code'
                
                script {
                    
                     dockerImage = docker.build branga9346 
                    
                }
                  
                
            } 
                
            }  
            
            
            stage('push') {
            steps {
                echo 'push image'
                script{
                    
                 docker.withRegistry( '', registryCredential ) {
                  dockerImage.push("$BUILD_NUMBER")
                  dockerImage.push('latest')
                 }}

          }
                
                
                
                
            }
        
        
        
        
        
        stage('Remove Unused docker image') {
steps{
sh "docker rmi $imagename:$BUILD_NUMBER"
sh "docker rmi $imagename:latest"
    
    
}}
        } 
        
        
        
        
        
        
        
    }
    
    

