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
              stage('buildx') {
                steps{
                    sh 'docker build -t ${IMAGEREPO}/buildx   --network=host buildx/.'
                    sh 'docker push ${IMAGEREPO}/buildx'
                }
              }

              stage('jenkins-controller') {
                steps{
                    sh 'docker build -t ${IMAGEREPO}/jenkins-controller   --network=host jenkins-controller/.'
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
              stage('test buildx') {
                steps{
                    sh 'docker image rm ${IMAGEREPO}/buildx'
                    sh 'docker run ${IMAGEREPO}/buildx'
                }
              }
            }
      }
  }

  environment {
    IMAGEREPO = 'registry.klucsik.fun'
  }

}