import groovy.io.FileType

def getFilesName() {
    def list = []

    def dir = new File(System.properties['java.io.tmpdir'])
    dir.eachFileRecurse (FileType.FILES) { file ->
        list << file.path
    }
    return list
}

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
  def shek = getFilesName()
  def kid = verify(shek)
  println(kid)
}
