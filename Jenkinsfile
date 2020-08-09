// Declarative pipelines must be enclosed with a "pipeline" directive.
pipeline {
    // This line is required for declarative pipelines. Just keep it here.
    agent any
    parameters {
        string(defaultValue: "TEST", description: 'What environment?', name: 'userFlag')
        choice(choices: ['US-EAST-1', 'US-WEST-2'], description: 'What AWS region?', name: 'region')
    }

    // This section contains environment variables which are available for use in the
    // pipeline's stages.
    environment {
	    region = "us-east-1"
    }
    
    // Here you can define one or more stages for your pipeline.
    // Each stage can execute one or more steps.
    stages {
        // This is a stage.
        stage('Example') {
            steps {
                // This is a step of type "echo". It doesn't do much, only prints some text.
                echo 'This is a sample stage'
		echo '${env}'
                // For a list of all the supported steps, take a look at
                // https://jenkins.io/doc/pipeline/steps/ .
            }
        }
    }
}
