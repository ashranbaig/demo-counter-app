pipeline{
    
    agent any 
    
    stages {
        
        stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/ashranbaig/demo-counter-app.git'
                }
            }
        }
        // stage('UNIT testing'){
            
        //     steps{
                
        //         script{
                    
        //             sh 'mvn test'
        //         }
        //     }
        // }
        // stage('Integration testing'){
            
        //     steps{
                
        //         script{
                    
        //             sh 'mvn verify -DskipUnitTests'
        //         }
        //     }
        // }
        stage('Maven build'){
            
            steps{
                
                script{


                    sh 'export MAVEN_HOME=/opt/maven'
                    sh 'export PATH=$PATH:$MAVEN_HOME/bin'
                    sh 'mvn --version'
                    sh 'mvn clean package'
                   // sh 'mvn clean install'
                }
            }
        }
        // stage('Static code analysis'){
            
        //     steps{
                
        //         script{
                    
        //             withSonarQubeEnv(credentialsId: 'sonar-api') {
                        
        //                 sh 'mvn clean package sonar:sonar'
        //             }
        //            }
                    
        //         }
        //     }
            // stage('Quality Gate Status'){
                
            //     steps{
                    
            //         script{
                        
            //             waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'
            //         }
            //     }
            // }
        }
        
}
