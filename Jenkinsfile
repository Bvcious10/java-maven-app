pipeline{
    agent any
    parameters{
        choice(name: 'version' choices:['1.1.0', '1.1.2', '1.1.3'])
    }
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
                echo "deploying the application ${params.version}"
            }
        }
    }


}