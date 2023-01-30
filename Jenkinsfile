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
                    credentialsId: '2c8aa812-0d33-4749-b40a-b1396ba347d5', 
                    groupId: "${mavenPom.groupId}", 
                    nexusUrl: '139.144.253.18:8081', 
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
