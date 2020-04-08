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
	   stage('Unzip jar file') {
			steps {
               script {
                 decompressFile(fileDirectory, fileName)
               }
            }
	   }
    }
}

def decompressFile(String path, String fileName) {
  dir (path) {
    echo "file decompression ${fileName}"
    bat 'dir'
	echo "here..."
    bat "tar -xf ${fileName}${tarExt}"
	echo "here...1"
	echo "heere2"
  }
}

