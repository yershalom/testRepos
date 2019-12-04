import groovy.io.FileType

def getFilesName() {
    def list = []
    def dir = new File(System.properties['java.io.tmpdir'])
    println("!!!!!!!!!!!!!!!!!!! $dir")
    dir.eachFile { file ->
        println(file.path)
        list.add(file.path)
    }
    return list
}

def envInput() {
    stage('env menu') {
        def choice = ["QA", "STG", "PROD"]
        def userInput = input(
            id: 'envInput', message: 'Please choose an Enviromant to deply!', parameters: [
            [$class: 'ChoiceParameterDefinition', choices: choice , description: 'user choose env to deploy to', name: 'envInput']
        ])
        return userInput
    }
}

def fileInput(filesName) {
    stage('files menu') {
        def userInput = input(
            id: 'fileInput', message: 'Please choose an file to deply!', parameters: [
            [$class: 'ChoiceParameterDefinition', choices: filesName , description: 'Choose file to deploy', name: 'fileInput']
        ])
        return userInput
    }
}

node {
  def filesName = getFilesName()
  echo "${filesName}"
  // def getEnv = envInput()
  // def getFileInput = fileInput(filesName)
  // println(getEnv)
  // println(getFileInput)
}
