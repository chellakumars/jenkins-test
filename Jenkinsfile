pipeline {
    agent any
    parameters {
        choice choices: ['Dev', 'Prod', 'Qa'], description: '', name: 'env'
    }
    echo "${env}"
    stages {
        stage("foo") {
            steps {
                echo "${env}"
            }
        }
    }
}
