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
        stage('Infostucture needs') {
        try {
            sh 'ping -c 1 -n -w 1 172.31.47.1 &> /dev/null'
        }
        catch (exc) {
            echo 'No pings!'
            ${TERRAFORM_NEEDS}='yes'
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