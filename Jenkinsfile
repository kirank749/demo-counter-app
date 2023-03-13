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
            stage('Quality Gate Status'){
                
                steps{
                    
                    script{
                        
                        waitForQualityGate abortPipeline: false, credentialsId: 'sonarqube token'
                    }
                }
            }
        stage('upload war file to Nexus'){
            steps{
                script{
                    def pom = readMavenPom file: 'pom.xml'
                    def nexusrepo= pom.version.endsWith("SNAPSHOT") ? "snapshots-maven" : "release-maven"
                    nexusArtifactUploader artifacts:
                        [
                            [
                                artifactId: 'springboot',
                                classifier: '', 
                                file: 'target/Uber.jar', 
                                type: 'jar']], 
                        credentialsId: 'nexus credentials',
                        groupId: 'com.example',
                        nexusUrl: '172.31.12.56:8081',
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        repository: nexusrepo,
                        version: "${pom.version}"
                }
            }
        }
        stage('Docker Image Build'){
            
            steps{
                
                script{
                    
                 sh'docker image build -t $JOB_NAME:v1.$BUILD_ID .'
                 sh'docker image tag $JOB_NAME:v1.$BUILD_ID kirank749:$JOB_NAME:v1.$BUILD_ID'
                 sh'docker image tag $JOB_NAME:v1.$BUILD_ID kirank749:$JOB_NAME:latest'   
                
                }
            }
        }
        }
        
}
