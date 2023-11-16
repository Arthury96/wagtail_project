// Pipeline block
pipeline {
   // Agent block
   agent any
   options {
      buildDiscarder(logRotator(numToKeepStr: '30'))
      timestamps()
   }
   parameters {
      string(
        name: "Branch_Name", 
        defaultValue: 'master', 
        description: ''
        )         
        string(
            name: "Image_Name", 
            defaultValue: 'manage_contact_app', 
            description: ''
        )    
        string(
            name: "Image_Tag", 
            defaultValue: 'latest', 
            description: 'Image tag'
        )       
    }
    // Stage Block
   stages {// stage blocks
      stage("Build and push docker image") {
         steps {
            script {
               def imageName = "${params.Image_Name}:${params.Image_Tag}"
               // sh "docker tag ${params.Image_Tag} http://pedantic_dirac:5000/${params.Image_Name}"
               docker.withRegistry('http://172.20.0.2:5000') {
                  def customImage = docker.build(imageName)
                  customImage.push()
               }  
            }
         }
      }
   }
}