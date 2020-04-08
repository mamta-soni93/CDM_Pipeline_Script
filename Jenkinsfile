#!/bin/sh
//app parmas
def fileDirectory="F:/InfoObjects/Jenkins/Download/test"
def fileName="test"
def tarExt=".tar.gz"
pipeline {
    agent any
	parameters {
		string(name: 'ADE_Version', defaultValue: '0.0.1', description: 'Project version, Needs to execute')
	}
    stages{
		stage('Push jar On Artifactory'){
            steps {
               //script {
               //  uploadArtifact()
              // }
			  echo "download jar file"
            }
       }
	   stage('Unzip jar file') {
			steps {
               script {
                 decompressFile(fileDirectory, fileName, tarExt)
               }
            }
	   }
    }
}

def uploadArtifact() {
bat '''
        curl -sSf -H "X-JFrog-Art-Api:AKCp5ekmsgbnFTK8mAWyiHq3W9q6KuDKGwBAjvNzvT5A2Vst1j4xHSZq3oPwC8V5jmLEqz3dQ" \
	   -o F:/InfoObjects/Jenkins/Download/test.tar.gz https://hexxa.jfrog.io/artifactory/Jenkins-integration/jb-hello-world-maven-0.1.0.jar
    '''
  echo "done"
}

def decompressFile(String path, String fileName, String tarExt) {
  dir (path) {
    echo "file decompression ${fileName}"
    bat 'dir'
	echo "here..."
    bat "tar -xf ${fileName}${tarExt}"
	echo "delete old compressed files ${fileName}"
    bat "del -f ${fileName}${tarExt}"  // sh "rm -f '${fileName}'"
    bat 'dir'
  }
}

