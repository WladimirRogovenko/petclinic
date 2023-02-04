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
                    sh 'ping -c 1 -n -w 1 172.31.47.1 &> /dev/null'
                }
                catch (exc) {
                    echo 'No pings to 172.31.47.1  -- TERRAFORM_NEEDS=yes'
                    TERRAFORM_NEEDS='yes'
                    build job: 'petclinic-terraform', parameters: [string(name: 'environment', value: "${GIT_BRANCH}")]
                }
                }
                echo "Ping result TERRAFORM_NEEDS = ${TERRAFORM_NEEDS}"
            }
        }
        /*
         stage('Terraform Job') {
            when {
                environment name: 'TERRAFORM_NEEDS', value: 'yes'
            }
            steps{
                echo "=== run Terraform main Job === "
                echo "TERRAFORM_NEEDS = ${TERRAFORM_NEEDS}"
                build job: 'petclinic-terraform', parameters: [string(name: 'environment', value: "${GIT_BRANCH}")]
            }
        } 
        */      
        stage('dev') {
            when {
                branch 'dev'
            }
            steps{
                echo "=== run dev stage - step 1 - BUILD ==="
                echo "TERRAFORM_NEEDS = ${TERRAFORM_NEEDS}"
                build job: 'petclinic-build', parameters: [string(name: 'environment_project', value: "${GIT_BRANCH}")]
                echo "=== finish dev stage - step 1 - BUILD ==="

                echo "=== run dev stage - step 2 - Deploy ==="
                build job: 'dev-CD-petclinic', parameters: [string(name: 'environment_project', value: "${GIT_BRANCH}")]
                echo "=== finish dev stage - step 2 - Deploy ==="
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