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
            git branch:'main', url:'https://github.com/kavin-bot/pythonargocd.git'
           }
        } 
   }
  }
}
