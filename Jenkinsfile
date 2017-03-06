#!groovy
podTemplate(label: 'demo', containers: [
    containerTemplate(name: 'jnlp', 
                      image: 'henryrao/jnlp-slave', 
                      args: '${computer.jnlpmac} ${computer.name}',
                      alwaysPullImage: true),
    containerTemplate(name: 'docker', 
                      image: 'docker:1.12.6', 
                      ttyEnabled: true, 
                      command: 'cat'),
  ],
  volumes: [ 
      hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock')
  ],
  workspaceVolume: persistentVolumeClaimWorkspaceVolume(claimName: 'jenkins-workspace', readOnly: false)
  ){
    node('demo'){
       checkout scm
       container('docker') {
         stage('build') {
           withDockerRegistry([url:"https://index.docker.io/v1/",credentialsId:"0e35e678-87fe-4090-af02-2e6deaf737d7"]) {
                docker.build("henryrao/jnlp-slave",'--pull .')
           }
         }
       }
       
       stage('test') {
           sh 'echo "testing"'
       }
       
       stage('deploy') {
           echo "${currentBuild.result}"
       }
    }
}
