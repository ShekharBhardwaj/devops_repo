pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }
        // publish the artifacts to nexus
        stage ('publish to nexus'){
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'devopsDemo', classifier: '', file: 'target/devopsDemo-0.0.11-SNAPSHOT.war', type: 'war']], credentialsId: 'newadmin', groupId: 'com.bhardwaj.devops', nexusUrl: '172.20.10.160:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'devops_repo-SNAPSHOT', version: '0.0.11-SNAPSHOT'
            }
        }

        // Stage3 : Publish the source code to Sonarqube
        stage ('Sonarqube Analysis'){
            steps {
                echo ' Source code published to Sonarqube for SCA......'
            }
        }

        
        
    }

}