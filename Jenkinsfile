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
  ]
  ){
    node('demo'){
       stage('build') {
           sh 'echo "compiling"'
       }
       
       stage('test') {
           sh 'echo "testing"'
       }
       
       stage('deploy') {
           echo "${currentBuild.result}"
       }
    }
}
