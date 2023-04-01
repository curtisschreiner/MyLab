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

        // Stage3: Publish the artifacts to Nexus
        stage ('Publish to Nexus'){
            steps {
                nexusArtifactUploader artifacts:
                [[artifactId: '${ArtifactId}',
                classifier: '',
                file: 'target/VinayDevOpsLab-0.0.4-SNAPSHOT.war',
                type: 'war']],
                credentialsId: 'c5ec9e0b-56a3-4895-b59f-5fc2fdf370ab',
                groupId: '${GroupId}',
                nexusUrl: '172.20.10.61:8081',
                nexusVersion: 'nexus3',
                protocol: 'http',
                repository: 'VinaysDevOpsLab-SNAPSHOT',
                version: '${Version}'
            }
        }

        // Stage 4 : Print some information
        stage ('Print Environment variables'){
                    steps {
                        echo "Artifact ID is '${ArtifactId}'"
                        echo "Version is '${Version}'"
                        echo "GroupID is '${GroupId}'"
                        echo "Name is '${Name}'"
                    }
                }

        // Stage5 : Publish the source code to Sonarqube
        stage ('Deploy'){
            steps {
                echo 'deploying....'

            }
        }

        
        
    }

}