def shek = ["Ynon", "Shalom", "Hila"]

def verify() {
    stage('Verify') {
        def userInput = input(
            id: 'userInput', message: 'This is PRODUCTION!', parameters: [
            [$class: 'ChoiceParameterDefinition', choices: shek, description: '', name: 'Choose kid']
        ])
        return userInput
    }
}

node {
  def kid = verify()
  println(kid)
}
