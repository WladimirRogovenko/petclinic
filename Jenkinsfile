//petclinic-dev
pipeline{
agent { label 'jenkins-master' }
options { timestamps ()        }
    stages {
        stage('Test') {
            steps{
                echo 'Branch name: ${BRANCH_NAME}  branch: ${GIT_BRANCH}'
                echo "Branch name: ${BRANCH_NAME}  branch: ${GIT_BRANCH}"
            }
        }
    }
} 