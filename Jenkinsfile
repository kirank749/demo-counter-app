pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                    
                    git branch: 'main', url: 'https://github.com/kirank749/demo-counter-app.git'
                }
        }
         stage('Unit Test'){

             steps{
                   
                   sh 'mvn test'

             }
        }
    }
}
