def verify() {
    stage('Verify') {
        def userInput = input(
            id: 'userInput', message: 'This is PRODUCTION!', parameters: [
            [$class: 'ChoiceParameterDefinition', choices: 'Choice 1\nChoice 2\nChoice 3', description: '', name: 'Choose Env']
        ])
    }
}

node {
  def stam = verify()
  println(stam)
}
