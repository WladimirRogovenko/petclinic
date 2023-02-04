//petclinic-dev
pipeline{
agent { label 'jenkins-master' }
options { timestamps ()        }
    stages {
        stage('Test') {
            steps{
                echo 'Branch name: ${env.BRANCH_NAME}'
            }
        }
    }
} 