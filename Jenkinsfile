node {
    agent any
    
    stages {
        stage('Build') {
            steps {
                echo "Listing contents of an S3 bucket."
                }
            }
        }    
    }
    post {
        success {
            echo "Build SUCCESS"
        }

        failure {
            echo "Build FAILED"
        }
    }
}
