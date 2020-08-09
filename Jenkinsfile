pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
        region = 'ap-south-1'
    }
    parameters {
        choice choices: ['Existing', 'New'], description: '', name: 'Repository'
        string defaultValue: '', description: '', name: 'Repo_ID', trim: true
        string defaultValue: '', description: '', name: 'url', trim: true
        string defaultValue: '', description: '', name: 'ACCOUNT_ID', trim: true
    }
    stages {
        stage('Build') {
            steps {
		script {    
			if (params.Repository == 'New') {
                    		sh "aws ecr create-repository --repository-name ${Repo_ID} --region ap-south-1"
                	} 
                	else {
	                	echo 'Using existing repo'
                	}
		}	
                echo "Listing contents of an S3 bucket."
                sh "git init"
                sh "rm -rf ecs-example"
                dir("ecs-example/") {
                    sh "whoami"
                    sh "git init"
                    echo "${url}"
                    sh "git clone ${url}"
                    dir("ecs-example/") {
                        sh "docker build -t ${Repo_ID} ."
                        sh "docker tag ${Repo_ID}:latest ${ACCOUNT_ID}.dkr.ecr.${region}.amazonaws.com/${Repo_ID}:latest"
                    }
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
