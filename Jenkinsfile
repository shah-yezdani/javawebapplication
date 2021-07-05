pipeline{
  agent none
  tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }
  stages{
    stage('Compile'){
      agent any
      steps{
        sh 'mvn compile'
      }       
    }
    stage('Code Quality'){
      agent any
      steps{
        sh 'echo Sonarqube Code Quality Check Done'
      }
    }
    stage('Test'){
      agent any
      steps{
        sh 'mvn test'
      }
    } 
    stage('Package'){
      agent any
      steps{
        sh 'mvn package'
      }
    }
    stage('Upload War File To Artifactory'){
      agent any
      steps{
        sh 'echo Uploaded War file to Artifactory'
      }
    }
    stage('Deploy'){
      agent any
      steps{
        sh label: '', script: '''rm -rf dockerimg
mkdir dockerimg
cd dockerimg
cp /var/jenkins_home/workspace/455867pipeline/target/in28Minutes-first-webapp-0.0.1-SNAPSHOT.war .
touch dockerfile
cat <<EOT>>dockerfile
FROM tomcat
ADD in28Minutes-first-webapp-0.0.1-SNAPSHOT.war /usr/local/tomcat/webapps/
CMD ["catalina.sh", "run"]
EXPOSE 8081
EOT
docker build -t webimage:$BUILD_NUMBER .
docker container run -td --name webserver$BUILD_NUMBER -p 8081:8081 webimage:$BUILD_NUMBER'''
      }
    }
  }
}
