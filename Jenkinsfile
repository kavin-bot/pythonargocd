pipeline{
agent any
  environment{
  DOCKER
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
           docker_image = docker.build "${IMAGE_NAME}" 
           }
        } 
   }
    stage('docker push')
    {
       steps
      {
        script
          {
            
           }
        } 
   }
  }
}
