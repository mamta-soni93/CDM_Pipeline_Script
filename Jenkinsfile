#!/bin/bash
# Instance for ADE deploy location 
def ADE_DEPLOY_LOCATION = "/data01/workspace/d1_deployment"
# Multiple instances of SDM can run within the same AWS account
def SDM_INSTALLATION_JAR_PATH="/data01/workspace/sdm_deployment/"

pipeline {
    agent any
	parameters {
		string(name: 'ADE_Version', defaultValue: '0.0.1', description: 'Project version, Needs to execute')
	}
    stages{
       stage('Push jar On Artifactory'){
            steps {
               script {
                 uploadArtifact()
               }
            }
       }
    }
}

def uploadArtifact() {
bat '''
        curl -sSf -H "X-JFrog-Art-Api:AKCp5ekmsgbnFTK8mAWyiHq3W9q6KuDKGwBAjvNzvT5A2Vst1j4xHSZq3oPwC8V5jmLEqz3dQ" \
       -X PUT \
       --form files="https://hexxa.jfrog.io/artifactory/Jenkins-integration/jb-hello-world-maven-0.1.0.jar" \
       "https://hexxa.jfrog.io/artifactory/SimpleMavenProject/jb-hello-world-maven-0.1.0.jar"
    '''
  echo "done"
}