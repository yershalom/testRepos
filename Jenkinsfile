def verify() {
    stage('Verify') {
        def userInput = input(
            id: 'userInput', message: 'This is PRODUCTION!', parameters: [
            [$class: 'ChoiceParameterDefinition', choices: 'Ynon\nShalom\nHila', description: '', name: 'Choose kid']
        ])
        return userInput
    }
}

node {
  def kid = verify()
  println(kid)
}
