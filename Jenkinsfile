def service = new com.ooyala.flex.jenkins.build.ansibleTest() as Object

service.build()
             
if (env.BRANCH_NAME == 'master') {
   build job: 'Environments/apply users role', wait: false
   build job: 'Packer/Jenkins slave image', wait: false
   build job: 'Packer/Base image multi-provider multi-region', wait: false
}