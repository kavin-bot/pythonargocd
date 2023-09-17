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

               docker build -t "${IMAGE_NAME}":${IMAGE_TAG} .
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
            withCredentials([usernamePassword(credentialsId: 'dockerkavin', passwordVariable: 'PASS', usernameVariable: 'USER')]) 
            {
              sh """ 
                docker login -u '$USER' -p '$PASS'
                docker push "${IMAGE_NAME}":${IMAGE_TAG}
                docker push "${IMAGE_NAME}:latest"
                """
            }
           // docker.withRegistry('',REGISTRY_CREDS)
            //docker_image.push("$BUILD_NUMBER")
            //docker_image.push('latest')
           }
        } 
   }
    stage('update the deployment file')
    {
       steps
      {
        script
          {
            sh"""
            cat deployment.yaml
            sed -i 's/${APP_NAME}.*/${APP_NAME}:${IMAGE_TAG}/g' deployment.yaml
            cat deployment.yaml
            """
           }
        } 
   }
    stage('update the ScM')
    {
       steps
      {
        script
          {
            sh"""
            git config --global user.name "kavin"
            git config --global user.email "creatingkavin@gmail.com"
            git add deployment.yaml
            git commit -am "update it"
            """
            withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
               git push "https://github.com/kavin-bot/pythonargocd.git"
}
           }
        } 
   }
  }
}

