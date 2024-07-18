pipeline{
    agent any

      tools{
        jdk 'jdk17'
        maven 'maven3'
      }
      environment{
        APP_NAME ="production-complite"
        RELEASE="1.0.0"
        DOCKER_USER="sanjay7794"
        DOCKER_PASS='docker'
        IMAGE_NAME="${DOCKER_USER}"+"/"+"${APP_NAME}"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"

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
               sh "mvn clean package  "
            }
        }
        stage("Test application"){
            steps{
               sh "mvn test"
            }
        }
        stage("Build and push docker image"){
            steps{
               script{
                docker.withRegistry('',DOCKER_PASS){
                    docker_image = docker.build "${IMAGE_NAME}"
                }
                docker.withRegistry('',DOCKER_PASS){
                    docker_image.push("${IMAGE_TAG}")
                    docker_image.push('latest')
                }
               }
            }
        }
    }
}