node{
    stage('Clone repo'){
    git credentialsId: 'git_credentials', url: 'https://github.com/riyaz1121/riyaz-task.git'
    }
 stage('Maven Build'){
                def mavenHome = tool name: "Maven-3.9.0", type: "maven"
                def mavenCMD = "${mavenHome}/bin/mvn"
                sh "${mavenCMD} clean package"
                }

                stage('SonarQube analysis') {
                withSonarQubeEnv('Sonar-Server-9.6.1') {
                def mavenHome = tool name: "Maven-3.9.0", type: "maven"
                def mavenCMD = "${mavenHome}/bin/mvn"
                sh "${mavenCMD} sonar:sonar"
                }
        }

                stage('upload war to nexus'){
                        nexusArtifactUploader artifacts: [
                        [
                                artifactId: 'pasha1',
                                classifier: '',
                                file: 'pasha1-3.0.7.jar',
                                type: 'war'
                                ]
                        ],
                                credentialsId: 'nexus3',
                                groupId: 'pasha',
                                nexusUrl: 'http://54.90.148.98:8081/repository/riyaz-release/',
                                nexusVersion: 'nexus3',
                                repository: 'riyaz-release/',
                                protocol: 'http',
                                version: '3.0.7'
                        }
        }
