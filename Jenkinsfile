pipeline {
    agent any
    def deployOptions = 'no\nyes'
    stages {

        stage('testing pipeline'){
          steps{
		    echo 'test1'
                sh 'mkdir from-jenkins'
                sh 'touch from-jenkins/test.txt'
                }
        }

}
}
