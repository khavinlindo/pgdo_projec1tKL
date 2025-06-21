pipeline {
    agent any
    
    tools {
        //To specify the maven to use
        maven "mvn3.9.9"
    }
    
    stages {
        stage('Checkout'){
            steps{
                //Checkout the source repo from scm
                git 'https://github.com/github-simplilearn-net/MavenBuild.git'
            }
        }
        stage('Build'){
            steps{
                //Use maven to build the project
                sh 'mvn clean package'
            }
        }
        stage('Test'){
            steps{
                //Run tests if applicable
                sh 'mvn test'
            }
        }
       stage ('Deploy the code'){
           steps{
               deploy adapters: [tomcat9(credentialsId: 'tomcat-id', path: '', url: 'http://localhost:9090/')], contextPath: null, war: '**/*.war'
           }
       }
        
    }
    post{
        success{
            //This will be executed if the pipeline execution is successful
            echo 'Pipeline executed successfully!'
        }
        failure{
            //This will be executed if the pipeline execution fails
            echo 'Pipeline failed!'
        }
    }
}
