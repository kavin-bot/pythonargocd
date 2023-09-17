pipeline{
agent any
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
            git credentialsId: 'github'
            url:'https://github.com/kavin-bot/pythonargocd.git'
            branch:'main'
           }
        } 
   }
  }
}
