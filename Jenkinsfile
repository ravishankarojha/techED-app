@Library('piper-library-os') _

node() {

  stage('prepare') {

      checkout scm

      echo ${GIT_COMMIT}
      
      setupCommonPipelineEnvironment script:this

           checkChangeInDevelopment script: this,changeDocumentId:'8000004822'     
    
       }

  stage('build') {
      mtaBuild script: this
      step([$class: 'UploadBuild',
      
             tenantId: "5ade13625558f2c6688d15ce",
      
             revision: "${GIT_COMMIT}",
      
             appName: "Sapphire 2019-SAP-Jenkins-Fiori-UI-Demo",
      
             requestor: "admin",
      
             id: "${BUILD_NUMBER}"
      
     ])
  }
}
