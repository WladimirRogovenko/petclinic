//petclinic-dev
pipeline{
agent { label 'jenkins-master' }
options { timestamps ()        }
environment {
    TERRAFORM_NEEDS='no'
}
    stages {
        stage('Test') {
            steps{
                echo "Branch name: ${BRANCH_NAME}  branch: ${GIT_BRANCH}"
            }
        }
        stage('Infrastucture needs') {
            steps{
                script{
                try {
                    sh 'ping -c 1 -n -w 1 8.8.8.8 &> /dev/null'
                    //172.31.47.1
                }
                catch (exc) {
                    echo 'No pings!'
                    TERRAFORM_NEEDS='yes'
                }
                }
                echo "123 TERRAFORM_NEEDS = ${TERRAFORM_NEEDS}"
            }
        }
        stage('dev') {
            when {
                branch 'dev'
            }
            steps{
                echo "run dev stage "
                echo "TERRAFORM_NEEDS = ${TERRAFORM_NEEDS}"
            }
        }
        stage('main') {
            when {
                //environment name: 'BRANCH_NAME', value: 'main'
                branch 'main'
            }
            steps{
                echo "run main stage "
            }
        }
    }
} 