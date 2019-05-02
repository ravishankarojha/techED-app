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
  }
}
