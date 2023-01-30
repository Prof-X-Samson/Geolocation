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
                    [[artifactId: '${POM_ARTIFACTID}', 
                    classifier: '', 
                    file: 'target/${POM_ARTIFACTID}-${POM_VERSION}.${POM_PACKAGING}', 
                    type: '${POM_PACKAGING}']],
                    credentialsId: '2c8aa812-0d33-4749-b40a-b1396ba347d5', 
                    groupId: '${POM_GROUPID}', 
                    nexusUrl: '139.144.253.18:8081/', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'biomedical', 
                    version: '${POM_VERSION}'
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
