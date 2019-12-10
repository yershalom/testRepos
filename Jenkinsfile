import groovy.io.FileType
import jenkins.model.Jenkins

def workingDir = "/var/lib/jenkins/workspace"

// function that pulls all the theme files to deploy depending on the environment choices.
@NonCPS
def getFilesName() {
    def list = []
    def dir = new File(workingDir)
    dir.eachFileRecurse (FileType.FILES) { file ->  
      if (file.path.contains(".zip") && !file.path.contains("@")) {
          def newFile = file.path.split("/")
        list << newFile[newFile.length -1]  
      }    
}
    def newList = list.sort()            
    return newList
}
// dropdown menu to choose the theme file to deploy.
def fileInput(filesName) {
    stage('files menu') {
        def userInput = input(
            id: 'fileInput', message: 'Please choose a file to deploy!', parameters: [
            [$class: 'ChoiceParameterDefinition', choices: filesName , description: '', name: 'fileInput']
        ])
        return userInput
    }
}
// dropdown menu to choose the deploy type:  single or mass.
def deployInput() {
    stage('Deploy Type'){
        def deploy = ['SINGLE', 'MASS']
        def serverInput = input(
            id: 'DEPLOY', message: 'Please choose mass or single', parameters:[
            [$class: 'ChoiceParameterDefinition', choices: deploy, description: 'Choose deploy type:  mass or single', name:'deployType' ]
            ])
            return serverInput
        }
}

node {
  def filesName = getFilesName()
  def getFileInput = fileInput(filesName)
  def getDeploy = deployInput()
  stage('get_Single_url') {
      if (params.deployType == 'SINGLE') {
          echo "is it single"
      } else {
          echo "it is mass deploy"
      }
 }
 // printing all choices to be used in single_mass bash script.
  echo "Choosen env is: $env_chooice"
  echo "Chosen theme to deploy: $theme"
  echo "Deploy type is: $getDeploy"
  
  // sh "/var/lib/jenkins/workspace/deploy_params.sh "
}
