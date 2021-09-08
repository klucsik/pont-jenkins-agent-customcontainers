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
                    sh 'docker build -t ${IMAGEREPO}/kubectl   --build-arg HTTP_PROXY=http://10.0.7.94:8080 --build-arg HTTPS_PROXY=http://10.0.7.94:8080 kubectl/.'
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

  environment {
    IMAGEREPO = 'k8stools.dev.pnt.hu:8443'
  }

}