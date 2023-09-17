pipeline{
agent any
  environment{
  DOCKERHUB_USERNAME= "dockerkavin"
  APP_NAME = "pythonapp"
  IMAGE_TAG= "${BUILD_NUMBER}"
  IMAGE_NAME= "${DOCKERHUB_USERNAME}" +"/"+"${APP_NAME}"
  REGISTRY_CREDS='dockerhub'
  }
  stages
  {
   stage('cleanup workspace')
    {
       steps
      {
        script
          {
            cleanWs()
           }
        } 
   }
    stage('checkouts')
    {
       steps
      {
        script
          {
            git branch:'main', url:'https://github.com/kavin-bot/pythonargocd.git'
           }
        } 
   }
    stage('docker build ')
    {
       steps
      {
        script
          {
           //docker_image = docker.build "${IMAGE_NAME}" 
            sh """

               docker build -t "${IMAGE_NAME}" .
               """
           }
        } 
   }
    stage('docker push')
    {
       steps
      {
        script
          {
            docker.withRegistry('',REGISTRY_CREDS)
            docker_image.push("$BUILD_NUMBER")
            docker_image.push('latest')
           }
        } 
   }
  }
}
