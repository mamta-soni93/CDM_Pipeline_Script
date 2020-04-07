#!/bin/bash
pipeline {
    agent any
	parameters {
		string(name: 'ADE_Version', defaultValue: '0.0.1', description: 'Project version, Needs to execute')
	}
    stages{
       stage('Printing'){
			steps {
                    echo "Here...."
					echo "${params.ADE_Version}"
				} 
      }
    }
}