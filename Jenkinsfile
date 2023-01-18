pipeline {
    agent any
    tools {
  maven 'M2_HOME'
}
    triggers {
 pollSCM ('*/2 * * * *')
}

    stages{
        stage("maven package"){
            steps{
             sh 'mvn clean'
             sh 'mvn install'
             sh 'mvn package'
            }
        }
              stage("test"){
            steps{
               sh 'mvn test'
            }
        }
              stage("Tester"){
            steps{
               echo 'Tested'
            }
        }
              stage("Deployment"){
            steps{
               echo 'Deploy'
            }
        }
    }
}