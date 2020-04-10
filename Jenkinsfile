#!/bin/bash
@Library('Application_SharedLibrary')_
// Jar file download location
def appDownloadJarLocation="F:/InfoObjects/Jenkins/Download/jar"
def fileName="hello-world"
def tarExtension=".tar.gz"
def jarExtension=".jar"
def admApp = "ADM"
def cdmApp = "CDM"
def global = "Global"
pipeline {
    agent any
	parameters {
		string(name: 'ADE_Version', defaultValue: '0.0.1', description: 'Need to ADM version')
		choice(name: 'Package_Type', choices: "$admApp\n$cdmApp\n$global", description: 'Defines the muliple application choices where one app will be deployed at a time')
		string(name: 'Tier', defaultValue: 'Drona', description: 'On which tier you want to deploy')
		string(name: 'CDM_Version', defaultValue: '0.0.1', description: 'Need to CDM version')
		string(name: 'Shared_Library_Branch', defaultValue: 'master', description: 'Groovy Script branch name')
		string(name: 'Artifactory_Credential_ID', description: 'Give credential ID of Artifactory repo')
	}
	stages{
	    stage('Download jar from artifactory') {
			steps {
			   echo "Download the application ${params.Package_Type}${params.ADE_Version} from artifactory"
               script {
                 downloadArtifact("${params.Artifactory_Credential_ID}")
               }
            }			
	    }
    }
}