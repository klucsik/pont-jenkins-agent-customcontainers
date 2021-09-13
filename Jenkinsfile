pipeline {
  agent {
    kubernetes {
      yamlFile 'jenkins-agent.yaml'
      defaultContainer 'docker'
    }
  }


  stages{
      stage('build and push images') {
            parallel {

              stage('kubectl') {
                steps{
                    sh 'docker build -t ${IMAGEREPO}/kubectl   --network=host kubectl/.'
                    sh 'docker push ${IMAGEREPO}/kubectl'
                }
              }

              stage('jenkins-controller') {
                steps{
                    sh 'docker build -t ${IMAGEREPO}/jenkins-in-cluster   --network=host jenkins-controller/.'
                    sh 'docker push ${IMAGEREPO}/jenkins-controller'
                }
              }

            }
      }

      stage('test pull and run images') {
            parallel {

              stage('test kubectl') {
                steps{
                    sh 'docker image rm ${IMAGEREPO}/kubectl'
                    sh 'docker run ${IMAGEREPO}/kubectl'
                }
              }

              stage('test jenkins controller') {
                steps{
                    sh 'docker image rm ${IMAGEREPO}/jenkins-controller'
                    sh 'docker run ${IMAGEREPO}/jenkins-controller'
                }
              }

            }
      }
  }

  environment {
    IMAGEREPO = 'k8stools.dev.pnt.hu:8443'
  }

}