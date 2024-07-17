pipeline{
    agent any

      tools{
        jdk 'jdk17'
        maven 'maven3'
      }

    stages{
        stage("Cleanup work space"){
            steps{
                cleanWs()
            }
        }
    
        stage("checkout from SCM"){
            steps{
               git branch: 'main', url:'https://github.com/sanjay7794/complete-prodcution-e2e-pipeline.git'
            }
        }
        stage("build application"){
            steps{
               sh "mvn clean packaeg"
            }
        }
        stage("Test application"){
            steps{
               sh "mvn test"
            }
        }
    }
}