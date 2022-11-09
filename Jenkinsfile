pipeline {
    agent any
    tools {
        maven "MAVEN3"
    }
    environment {
        SNAP_REPO = 'test_snap'
		NEXUS_USER = 'admin'
		NEXUS_PASS = 'admin'
		RELEASE_REPO = 'release_repository'
		NEXUSIP = '172.31.43.101'
		NEXUSPORT = '8081'
		NEXUS_GRP_REPO = 'maven_groups'
        NEXUS_LOGIN = 'nexuslogin'
        registryCredential = "${NEXUS_LOGIN}"
    }
    stages {
        stage('Clone') {
            steps {
                sh "git clone https://github.com/VarshithaSane/maven-project.git"
            }
            post {
                success {
                    echo "Now Archiving."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Build') {
            steps {
                sh "mvn clean install"
            }
        }
        // stage("UploadArtifact"){
        //     steps{
        //         nexusArtifactUploader(
        //           nexusVersion: 'nexus3',
        //           protocol: 'http',
        //           nexusUrl: "${NEXUSIP}:${NEXUSPORT}",
        //           groupId: 'QA',
        //           //version: "${params.SERVICE_NAME}-10.1.66-${env.BUILD_ID}-${env.BUILD_TIMESTAMP}",
        //           repository: "${RELEASE_REPO}",
        //           credentialsId: "${NEXUS_LOGIN}",
        //           artifacts: [
        //             [artifactId: 'sample_id',
        //              classifier: '',
        //              file: "maven-project/webapp/target/webapp.war",
        //              //file: "Services/${params.SERVICE_NAME}/target/${params.SERVICE_NAME}/${params.SERVICE_NAME}-exec.jar",
        //              type: 'war']
        //           ]
        //         )
        //     }
        // }
    }
}