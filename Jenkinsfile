#!/bin/bash
@Library('Application_SharedLibrary')_
// Jar file download location
def appDownloadJarLocation="F:/InfoObjects/Jenkins/Download/jar"
def fileName="hello-world"
def tarExtension=".tar.gz"
def admApp = "ADM"
def sdmApp = "SDM"
def global = "Global"
pipeline {
    agent any
	parameters {
		string(name: 'APP_Version', defaultValue: '0.0.1', description: 'Need to add project version')
		choice(name: 'APP_Name', choices: "$admApp\n$sdmApp\n$global", description: 'Defines the muliple application choices where one app will be deployed at a time')
	}
	stages{
	    stage('Download jar from artifactory') {
			steps {
			   echo "Download the application ${params.APP_Name}${params.APP_Version} from artifactory"
               script {
                 downloadArtifact()
               }
            }			
	    }
	    stage('Zip jar file') {
			steps {
			   echo "Zip a jar file in extensio : ${tarExtension}"
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
							--packageType=${params.APP_Name}
						"""
					}
               }
			 echo "Deployment Done...!!"
            }			
	   }
    }
}

// File Downloading method
def downloadArtifact() {
	bat '''
        curl -sSf -H "X-JFrog-Art-Api:AKCp5ekmsgbnFTK8mAWyiHq3W9q6KuDKGwBAjvNzvT5A2Vst1j4xHSZq3oPwC8V5jmLEqz3dQ" \
	   -o F:/InfoObjects/Jenkins/Download/test.jar https://hexxa.jfrog.io/artifactory/Jenkins-integration/jb-hello-world-maven-0.1.0.jar
    '''
	echo "Jar file downloading is complete"
}

// Zip a jar file
def zipJarFile() {
	bat '''
        curl -sSf -H "X-JFrog-Art-Api:AKCp5ekmsgbnFTK8mAWyiHq3W9q6KuDKGwBAjvNzvT5A2Vst1j4xHSZq3oPwC8V5jmLEqz3dQ" \
	   -o F:/InfoObjects/Jenkins/Download/test.tar.gz https://hexxa.jfrog.io/artifactory/Jenkins-integration/jb-hello-world-maven-0.1.0.jar
    '''
	echo "Jar file zip is completed"
}