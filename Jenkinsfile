pipeline{
    agent any
    stages{
        stage('build'){
            steps{
                echo 'building the application'
            }
        }
        stage('test'){
            steps{
                echo 'testing the application'
                echo "${env.BUILD_ID}-${env.GIT_COMMIT}"
            }
        }
        stage('deploy'){
            steps{
                echo 'deploying the application'
            }
        }
    }


}