//petclinic-dev
pipeline{
agent { label 'jenkins-master' }
options { timestamps ()        }
    stages {
        stage('Test') {
            steps{
                echo "Branch name: ${BRANCH_NAME}  branch: ${GIT_BRANCH}"
            }
        }
        stage('dev') {
            when {
                branch 'dev'
            }
            steps{
                echo "run dev stage "
            }
        }
        stage('dev2') {
            when {
                expression {
                    return env.BRANCH_NAME == 'dev';
                }
            }
            steps{
                echo "run dev2 stage "
            }
        }
        stage('main') {
            when {
                environment name: 'BRANCH_NAME', value: 'main'
            }
            steps{
                echo "run main stage "
            }
        }
    }
} 