pipeline {
    agent any
    tools {
  maven 'M2_HOME'
}
    stages{
        stage("maven package"){
            steps{
             sh 'mvn clean'
             sh 'mvn install'
             sh 'mvn package'
            }
        }
              stage("artifact upload"){
            steps{
               script{
                    def mavenPom = readMavenPom file: 'pom.xml'
                    nexusArtifactUploader artifacts: 
                    [[artifactId: "${mavenPom.artifactId}", 
                    classifier: '', 
                    file: "target/${mavenPom.artifactId}-${mavenPom.version}.${mavenPom.packaging}", 
                    type: "${mavenPom.packaging}"]],
                    credentialsId: 'Nexus_id', 
                    groupId: "${mavenPom.groupId}", 
                    nexusUrl: '192.168.64.64:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'biomedical', 
                    version: "${mavenPom.version}"
                }
            }
        }
              stage("Deployment"){
            steps{
               echo 'Deploy'
            }
        }
    }
}
