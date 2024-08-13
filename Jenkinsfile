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
        stage('SonarQube Analysis') {
            steps{
                  sh "mvn clean verify sonar:sonar \
  -Dsonar.projectKey=java-app \
  -Dsonar.projectName='java-app' \
  -Dsonar.host.url=http://172.21.21.122:9000 \
  -Dsonar.token=sqp_5c61a7d1ec486e1ccace96b25037e6c0b55858cd"
            }
  }
  
        // stage('build docker image'){
        //     steps{
        //         sh "docker build -t ${IMAGE_REPO}/${NAME}:${VERSION} ."
                
        //     }
        // }
        // stage('deploy to docker repository'){
        //     steps{
        //         withDockerRegistry([credentialsId: 'docker-hub', url:'']){
        //             sh "docker push ${IMAGE_REPO}/${NAME}:${VERSION}"
        //         }
        //     }
        // }
    }
    }
