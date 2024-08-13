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
    stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    // Optionally use a Maven environment you've configured already
                    withMaven(maven:'Maven 3.5') {
                        sh 'mvn clean package sonar:sonar'
                    }
                    timeout(time: 2, unit: 'MINUTES') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    waitForQualityGate abortPipeline: true
                }
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
