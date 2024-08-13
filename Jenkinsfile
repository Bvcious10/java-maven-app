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
                withSonarQubeEnv('SonarQube'){
                                sh "mvn clean verify sonar:sonar \
  -Dsonar.projectKey=java-app \
  -Dsonar.projectName='java-app' \
  -Dsonar.host.url=http://172.21.21.122:9000"
   }
    timeout(time: 2, unit: 'MINUTES') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    waitForQualityGate abortPipeline: true
                }
            }
  }
        stage('Vulnerability scan'){
            steps{
                sh "mvn dependency-check:check"
            }
            post{
                always{
                    dependencyCheckPublisher pattern: 'target/dependency-check-report.xml'
                }
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
