pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        region = 'ap-south-1'
    }
    parameters {
        choice choices: ['Dev', 'Prod', 'Qa'], description: '', name: 'env'
        string defaultValue: '', description: '', name: 'Repo_ID', trim: true
        string defaultValue: '', description: '', name: 'GIT_url', trim: true
        string defaultValue: '', description: '', name: 'ACCOUNT_ID', trim: true
    }
    stages {
        stage('Build') {
            steps {
                echo "Listing contents of an S3 bucket."
                sh "git init"
                sh "rm -rf ecs-example"
                sh "git init"
                sh "git clone ${GIT_url}"
                dir("ecs-example/") {
                    sh "whoami"
                    sh "docker build -t ${Repo_ID} ."
                    sh "docker tag ${Repo_ID}:latest ${ACCOUNT_ID}.dkr.ecr.${region}.amazonaws.com/${Repo_ID}:latest"
                }
            }
        }    
        stage("Push"){
            steps {
                dir("kawatch-backend/") {
                    sh "eval \$(aws ecr get-login --region ap-south-1 --no-include-email)"
                    sh "docker images"
                    sh "docker push ${ACCOUNT_ID}.dkr.ecr.${region}.amazonaws.com/${Repo_ID}:latest"
                    sh "docker rmi -f ${ACCOUNT_ID}.dkr.ecr.${region}.amazonaws.com/${Repo_ID}:latest"
                }
            }
        }
    }
    post {
        success {
            echo "Build SUCCESS"
            //sh "docker images -q -a | xargs --no-run-if-empty docker rmi -f"
        }

        failure {
            echo "Build FAILED"
        }
    }
}
