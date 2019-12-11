import groovy.io.FileType
import jenkins.model.Jenkins

env.workingDir = "/tmp/"

// function that pulls all the theme files to deploy depending on the environment choices.
@NonCPS
def getFilesName() {
    def list = []
    def dir = new File(workingDir + env_choice)
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
// dropdown menu to choose the deploy type: single or mass.
def deployInput() {
    stage('Deploy Type'){
        def deploy = ['SINGLE', 'MASS'] //array for deploy type
        def serverInput = input(
            id: 'deployType', message: 'Please choose mass or single', parameters:[
            [$class: 'ChoiceParameterDefinition', choices: deploy, description: 'Choose deploy type: mass or single', name:'deployType' ]
        ])
        return serverInput
    }
}
node {
    def filesName = getFilesName()
    def getFileInput = fileInput(filesName)
    def getDeploy = deployInput()
    stage('get_Single_url') {
        def inputUrl
        if (deployInput == "single") { //this if is to open a text box to get url to single deploy. if the input of serverDeploy == single open a text box. its not working right
            def singleUrl = input(
                id: 'singleUrl', message: 'enter url address for single deploy:',
                parameters: [
                    [$class: 'StringParameterDefinition',defaultValue: 'None',
                     description: 'url address for single deployment',
                     name: 'Url'],
                ])

            echo ("single url is: "+singleUrl)
        }
// printing all choices to be used in single_mass bash script.
        echo "Choosen env is: $env_choice"
        echo "chosen theme file is: $getFileInput"
        echo "Chosen theme to deploy: $theme"
        echo "Deploy type is: $getDeploy"

// sh "/var/lib/jenkins/workspace/deploy_params.sh "
    }
}
