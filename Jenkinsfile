node {
  def myGradleContainer = docker.image('cdovidio/gradle-jdk8-node
')
  myGradleContainer.pull()
  stage('prep') {
    checkout scm
  }
  stage('test') {
     myGradleContainer.inside("-v ${env.HOME}/.gradle:/home/gradle/.gradle") {
       sh 'cd complete && gradle test'
     }
  }
  stage('run') {
     myGradleContainer.inside("-v ${env.HOME}/.gradle:/home/gradle/.gradle") {
       sh 'cd complete && gradle run'
     }
  }
}
