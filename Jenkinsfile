pipeline{
 agent none
  stages{
    stage('Compile'){
      agent any
      steps{
        sh 'mvn compile'
      }
      stage('Test'){
      agent any
      steps{
        sh 'mvn test'
      }
        stage('Pakage'){
      agent any
      steps{
        sh 'mvn package'
      }
          stage('Deploy'){
      agent any
      steps{
        sh label: '', script: '''rm -rf dockerimg
        mkdir dockerimg
        cd dockerimg
        cp 
      }
            
}
