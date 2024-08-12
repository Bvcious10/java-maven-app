pipeline{
    agent any
    environment{
        NAME = "java-app"
        VERSION = "${env.BUILD_ID}-${env.GIT_COMMIT}"
        IMAGE_REPO = "benvic"
    }
    tools{
        maven 'Maven'
    }
    stages{
        stage('build jar'){
            steps{
                echo 'building the application'
                sh 'mvn package'
            }
        }
        stage('build docker image'){
            steps{
                sh "docker build -t ${IMAGE_REPO}/${NAME}:${VERSION} ."
                
            }
        }
        stage('deploy to docker repository'){
            steps{
                withDockerRegistry([credentialsId: 'docker-hub', url:'']){
                    sh "docker push ${IMAGE_REPO}/${NAME}:${VERSION}"
                }
            }
        }
    }
    }
