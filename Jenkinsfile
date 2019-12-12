import groovy.io.FileType
import jenkins.model.Jenkins

env.workingDir = "/tmp/"
env.wcmsPluginsDir = "/var/lib/jenkins/workspace/WCMS_PLUGINS"
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
// dropdown menu to choose the wcms plugin to install
def wcmsPlugins() {
    stage('wcms plugins') {
        def wcmsPlugins = input (
            id: 'wcmsInput', message: 'Will deploy include wcms spacial plugins?', parameters: [
            [$class: 'BooleanParameterDefinition', defaultValue: false, description: 'Check box to also install wcms spacial plugins', name: 'wcmsInput']
        ])
        return wcmsPlugins
        echo ("wcms plugin is:"+wcmsInput)
    }
}// dropdown menu to choose the external plugin to install
def externalPlugins() {
    stage('External plugins') {
        def externalPlugins = input (
            id: 'externalPlugins', message: 'Will the deploy include external plugins?', parameters: [
            [$class: 'BooleanParameterDefinition', defaultValue: false, description: 'Check box to also install external plugins', name: 'externalPlugins']
        ])
        return wcmsPlugins
        echo ("wcms plugin is:"+wcmsInput)
    }
}
// dropdown menu to choose the deploy type:  single or mass.
def deployInput() {
    stage('Deploy Type'){
        def deploy = ['SINGLE', 'MASS'] //array for deploy type
        def serverInput = input(
            id: 'deployType', message: 'Please choose mass or single', parameters:[
            [$class: 'ChoiceParameterDefinition', choices: deploy, description: 'Choose deploy type:  mass or single', name:'deployType' ]
        ])
        return serverInput
    }
}
node {
    def filesName = getFilesName()
    def getFileInput = fileInput(filesName)
    def getDeploy = deployInput()
    //def getWcms = wcmsPlugins()
    stage('get_Single_url') {
        def inputUrl
        if (getDeploy == "SINGLE") {
            def singleUrl = input(
                id: 'singleUrl', message: 'enter url address for single deploy:',
                parameters: [
                    [$class: 'StringParameterDefinition',defaultValue: '',
                     description: 'url address for single deployment',
                     name: 'Url'],
                ])

            echo ("single url is: "+singleUrl)
        }
    }

    // printing all choices to be used in single_mass bash script.
    echo "Choosen env is: $env_choice"
    echo "chosen theme file is: $getFileInput"
    echo "Chosen theme to deploy: $theme"
    echo "Deploy type is: $getDeploy"
    echo "it will deply with wcms plugins: $getWcms"
}
