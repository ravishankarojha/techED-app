@Library('piper-library-os') _

node() {

  stage('prepare') {

      checkout scm

      setupCommonPipelineEnvironment script:this

           checkChangeInDevelopment script: this,changeDocumentId:'8000004822'     
    
       }

  stage('build') {
      mtaBuild script: this
    dir(srcDir){
  sh 'cdr=$(pwd); $cdr/jenkins.sh "build.sh"'
}
  }

  stage('neoDeploy') {
      neoDeploy script: this
  }

  stage('solmanTrCreate') {
      transportRequestCreate script:this, changeDocumentId:'8000004822',developmentSystemId: 'SM1~ABAP/001',applicationId: 'HCP'
  }
  stage('solmanUpload') {
      transportRequestUploadFile  script:this, changeDocumentId:'8000004822',developmentSystemId: 'SM1~ABAP/001',applicationId: 'HCP'
  }
}
