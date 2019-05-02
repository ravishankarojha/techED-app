@Library('piper-library-os') _

node() {
  
  def check
  stage('prepare') {
      check=checkout scm
      echo "${check}"
      setupCommonPipelineEnvironment script:this
      checkChangeInDevelopment script: this,changeDocumentId:'8000004822'     
      echo ">>>>>>>${check.GIT_COMMIT}"
       }

  stage ("build") {
                step([$class: 'UCDeployPublisher', 
                                                component: [
                                                                componentName: 'Sapphire2019SAP',
                                                                componentTag: '',
                                                                delivery: [
                                                                                $class: 'Push',
                                                                                baseDir: "/var/lib/jenkins/workspace/Sapphire-2019-SAP-Demo/build-ucd",
                                                                                fileExcludePatterns: '',
                                                                                fileIncludePatterns: '**/*',
                                                                                pushDescription: '',
                                                                                pushIncremental: false,
                                                                                pushVersion: "${BUILD_NUMBER}"]
                                                ]])
                                                
                                newComponentVersionId = "${Sapphire2019SAP_VersionId}"
                                echo "Component Version ID =>>>>>>>${newComponentVersionId}"
        step([$class: 'UploadBuild',
           tenantId: "5ade13625558f2c6688d15ce",
           revision: "${check.GIT_COMMIT}",
           appName: "Sapphire 2019-SAP-UrbanCode-ABAP-BE-Demo",
           requestor: "admin",
           id: "${newComponentVersionId}"
        ])
   }


stage('Publish to UrbanCode Deploy') {        
                sleep 15
                                step([$class: 'UCDeployPublisher', 
                                                deploy: [
                                                                createSnapshot: [
                                                                                deployWithSnapshot: true,
                                                                                snapshotName: "${BUILD_NUMBER}"],
                                                                                deployApp: 'Sapphire 2019-SAP-UrbanCode-ABAP-BE-Demo',
                                                                                deployDesc: 'Requested from Jenkins',
                                                                                deployEnv: 'DEV',
                                                                                deployOnlyChanged: false,
                                                                                deployProc: 'deploy',
                                                                                deployReqProps: '',
                                                                                deployVersions: "Sapphire2019SAP:${BUILD_NUMBER}"]])
                }

}
