pipeline {
  agent {
    kubernetes {
      yamlFile 'k8s/agents/jenkins-agent.yaml'
      defaultContainer 'docker'
    }
  }


  stages{
      stage('build and push images') {
            parallel {

              stage('kubectl') {
                steps{
                    sh 'docker build -t ${IMAGEREPO}/kubectl /kubectl/.'
                    sh 'docker push ${IMAGEREPO}/kubectl'
                }

              }

            }
      }

      stage('test pull and run images') {
            parallel {

              stage('test kubectl') {
                steps{
                    sh 'docker iamge rm ${IMAGEREPO}/kubectl'
                    sh 'docker run ${IMAGEREPO}/kubectl'
                }


              }

            }
      }
  }

  envrionment{
    IMAGEREPO = 'k8stools.dev.pnt.hu:8443'
  }

}