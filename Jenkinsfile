node
{
def mavenHomeDirectory = tool name: 'Maven 3.9.9'
properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '10', daysToKeepStr: '', numToKeepStr: '10')), pipelineTriggers([pollSCM('*/1 * * * *')])])
stage('get the code from github ')
{
git credentialsId: '3f6dcac6-a25e-43ec-8cfa-6c0342371d3d', url: 'https://github.com/kotaRamyapriya/maven-web-application.git'
}
stage('creating build package')
{
 sh "${mavenHomeDirectory}/bin/mvn clean package"
}
stage('creating sonarqube report')
{
 sh "${mavenHomeDirectory}/bin/mvn sonar:sonar"
}
stage('upload build package into nexus')
{
 sh "${mavenHomeDirectory}/bin/mvn deploy"
}
/*stage('deploy into tomcat')
{
deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'da67adc0-b05d-4faf-96ce-21aead1742d4', path: '', url: 'http://52.224.240.205:8080/')], contextPath: 'maven-web-application', onFailure: false, war: 'target/maven-web-application.war'

}*/
}
