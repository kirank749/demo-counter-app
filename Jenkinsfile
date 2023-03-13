pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/kirank749/demo-counter-app.git'
                }
            }
        }
        stage('UNIT testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn test'
                }
            }
        }
        stage('Integration testing'){
            
            steps{
                
                script{
                    
                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }
        stage('Maven build'){
            
            steps{
                
                script{
                    
                    sh 'mvn clean install'
                }
            }
        }
        stage('Static code analysis'){
            
            steps{
                
                script{
                    
                    withSonarQubeEnv(credentialsId: 'sonarqube token') {
                        
                        sh 'mvn clean package sonar:sonar'
                    }
                   }
                    
                }
            }
        stages('artifact uploading to Nexus Repository'){
            
            steps{
                script{
                  nexusArtifactUploader credentialsId: 'nexus credentials', groupId: '1', nexusUrl: '3.110.90.82:8081/repository', nexusVersion: 'nexus3', protocol: 'http', repository: 'snapshots-maven', version: '1' 
                    {    
                        sh 'mvn deply'
                    }
                }
            }
                
        }                                            
                                                       
        
            
        }
        
}
