node{
def mavenhome = tool name: "maven 3.8.5"
//checkout stage
stage('checkout stage'){
git branch: 'development', credentialsId: 'dc016870-29b0-437b-b667-a4886bbabe5e', url: 'https://github.com/munnaelevator/maven-web-application.git'
}
//build stage
stage('build'){
sh "$mavenhome/bin/mvn clean package"
}
//generate sonarqube report
stage ('sonar qube report'){
sh "$mavenhome/bin/mvn sonar:sonar"


}
//upload artifact into artifactory repo
stage ('uploadartifactsintonexus'){
sh "$mavenhome/bin/mvn deploy"
}
//Deploy app into tomcat server
  stage ('Deployappinto tomcat'){
sshagent(['48a7e6eb-8db2-40d3-92b5-b08a655491a9']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@18.191.255.83:/opt/apache-tomcat-9.0.59/webapps"
}
}
}//node closing
