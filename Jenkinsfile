node{
    def mavenHome = tool name: "maven3.9.6"
//checkout code
stage('CheckoutDode'){
 git branch: 'development', credentialsId: '12f4826f-63d9-4d76-b1da-3033d6ea4167', url: 'https://github.com/prasanthnn/maven-web-application.git'
}
//build stage
stage('Build'){
sh " $mavenHome/bin/mvn clean package "

}
//generate sonarqube report
stage('sonarQubeReport'){
sh "$mavenHome/bin/mvn sonar:sonar"
}
//upload artifact into artifactory report
stage ('uploadartifactintonexus'){
sh "$mavenHome/bin/mvn deploy"
}
//deploy app into tomcat seerver
stage('DeployAppIntoTomcat'){
sshagent(['be84c473-8301-4a5f-98c4-d5436af982fa']) {
 sh "scp -o  StrictHostKeyChecking=no target/maven-web-application.war ec2-user@3.108.249.113:/opt/apache-tomcat-9.0.83/webapps"
}
}

} //node closing
