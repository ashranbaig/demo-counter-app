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
        //                def mvnHome = tool name: 'Maven', type: 'maven'
        //             sh "${mvnHome}/bin/mvn -B -DskipTests test"
        //            // sh 'mvn test'
        //         }
        //     }
        // }
        // stage('Integration testing'){
            
        //     steps{
                
        //         script{
        //                def mvnHome = tool name: 'Maven', type: 'maven'
        //             sh "${mvnHome}/bin/mvn -B -DskipTests verify -DskipUnitTests"
        //             //sh 'mvn verify -DskipUnitTests'
        //         }
        //     }
        // }
        stage('Maven build'){
            
            steps{
                
                script{
                    
                    def mvnHome = tool name: 'Maven', type: 'maven'
                    sh "${mvnHome}/bin/mvn -B -DskipTests clean install"
                   //sh 'mvn clean install'

                    
                }
            }
        }
        stage('Static code analysis'){
            
            steps{
                
                script{
                    
                    withSonarQubeEnv(credentialsId: 'DemoFinal') {
                     def mvnHome = tool name: 'Maven', type: 'maven'
                    sh "${mvnHome}/bin/mvn -B -DskipTests clean package sonar:sonar"

                        
                       // sh 'mvn clean package sonar:sonar'
                    }
                   }
                    
                }
            }
            stage('Quality Gate Status'){
                
                steps{
                    
                    script{
                        
                        waitForQualityGate abortPipeline: false, credentialsId: 'DemoFinal'
                    }
                }
            }


        stage('Upload war file to nexus'){
            
            steps{
                
                script{
                    
                       nexusArtifactUploader artifacts: 
                           [
                               [artifactId: 'springboot',
                                classifier: '',
                                file: 'target/Uber.jar', 
                                type: 'jar']],
                               credentialsId: 'nexus-auth',
                               groupId: 'com.example',
                               nexusUrl: '13.50.113.195:8081/',
                               nexusVersion: 'nexus3',
                               protocol: 'http',
                               repository: 'demoapp-release',
                               version: '1.0.0'   
                    }
                   }
                    
                }
            }
    
    
    }
    
    
