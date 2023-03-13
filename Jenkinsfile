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
         stage('Unit Test'){

             steps{

              script{
                   
                   sh 'mvn test'

                }
             }
        }
    }
}
