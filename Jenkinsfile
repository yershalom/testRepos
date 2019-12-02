def verify(shek) {
    stage('Verify') {
        def userInput = input(
            id: 'userInput', message: 'This is PRODUCTION!', parameters: [
            [$class: 'ChoiceParameterDefinition', choices: shek, description: '', name: 'Choose kid']
        ])
        return userInput
    }
}

node {
  def shek = ["Ynon", "Shalom", "Hila"]
  def kid = verify(shek)
  println(kid)
}
