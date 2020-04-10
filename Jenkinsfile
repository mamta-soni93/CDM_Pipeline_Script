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
		string(name: 'Artifactory_Credential_ID', description: 'Give credential ID of Artifactory id')
	}
	stages{
	    stage('Download jar from artifactory') {
			steps {
			   echo "Download the application ${params.Package_Type}${params.ADE_Version} from artifactory"
               script {
                 downloadArtifact()
               }
            }			
	    }
	    stage('Zip jar file') {
			steps {
			   echo "Zip a jar file in extension : ${tarExtension}"
               script {
                 zipJarFile()
               }
            }			
	    }
	    stage('UnZip jar file') {
			steps {
			   echo "UnZip a jar file and delete old one"
               script {
                 unZipTarFile(appDownloadJarLocation, fileName, tarExtension)
               }
            }			
		}
	    stage('Deploy a jar file') {
			steps {
			   echo "Deployment...!!"
               script {
                 dir(appDownloadJarLocation) {
						bat 'dir'
						bat """
							java -jar ${fileName}.jar \
							--application ${appDownloadJarLocation}/resources/application.yml \
							--var "awsAccessKey=t12345" \
							--packageType=${params.Package_Type}
						"""
					}
               }
			 echo "Deployment Done...!!"
            }			
	    }
		stage('Remove a jar file') {
			steps {
               script {
                 removingFile(appDownloadJarLocation, fileName, jarExtension)
               }
            }			
	    }
    }
}