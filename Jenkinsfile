pipeline {
    agent any
    tools {
        maven 'M2-HOME'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
            }
        }
        stage('Upload War To Nexus'){
            steps{
                script{  
                   nexusArtifactUploader artifacts: [
                       [
                            artifactId: 'vijaynexus',
                            classifier: '',
                            file: "target/vijaynexus-1.0.0-SNAPSHOT.war",
                            type: 'war'
                           ]
                       ],
                    credentialsId: 'Nexus3',
                    groupId: 'in.javahome',
                    nexusUrl: '192.168.33.10:8081',
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    repository: 'nexrepo',
                    version: '1.0.0'
              }
            }
        }
    }
}
