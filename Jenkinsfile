node {
        def deployOptions = 'no\nyes'
        def userInput = input(
          id: 'userInput', message: 'Are you prepared to deploy?', parameters: [
          [$class: 'ChoiceParameterDefinition', choices: deployOptions, description: 'Approve/Disallow deployment', name: 'deploy-check']
          ]
        )
        echo "you selected: ${userInput}"
    }
