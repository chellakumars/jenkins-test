pipeline {
    agent any
    parameters {
        choice choices: ['Dev', 'Prod', 'Qa'], description: '', name: 'env'
        string defaultValue: '', description: '', name: 'Please enter the repository name :', trim: true
    }

    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'sqlite'
    }

    stages {
        stage('Build') {
            steps {
                echo "Database engine is ${DB_ENGINE}"
                echo "DISABLE_AUTH is ${DISABLE_AUTH}"
                echo "ENV ${env}"
                sh 'printenv'
            }
        }
    }
}
