pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }
    environment{
        ArtifactId = readMavenPom().getArtifactId()
        Version = readMavenPom().getVersion()
        Name = readMavenPom().getName()
        GroupId = readMavenPom().getGroupId()
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
                script {
                def NexusRepo = Version.endsWith("SNAPSHOT") ? "devops_repo-SNAPSHOT" : "devops_repo-RELEASE"
                nexusArtifactUploader artifacts: 
                [[artifactId: "${ArtifactId}", 
                classifier: '', 
                file: "target/${ArtifactId}-${Version}.war", 
                type: 'war']], 
                credentialsId: 'newadmin', 
                groupId: "${GroupId}", 
                nexusUrl: '172.20.10.160:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: "${NexusRepo}", 
                version:  "${Version}"
                }
            }
        }

        stage ('print the information'){
            steps {
                echo "Artifact ID is '${ArtifactId}'"
                echo "Version number is '${Version}'"
                echo "Name is '${Name}'"
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