def branch = "main"
def repo = "https://github.com/angellaviory/dumbmerchbe"
def cred = "ubuntu"
def dir = "~/dumbmerchbe"
def server = "192.168.64.49"
def imagename = "dumbmerchbe"

pipeline {
	agent any
	stages {
		stage ('Pull From Git'){
			steps{
				sshagent ([credi]) {
					sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
					cd ${dir}
					git pull ${branch}
					exit
					EOF"""
				}
			}
		}
	

        stage('Image Build') {
            steps {
                sshagent([cred]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    mkdir ${dir}
                    cd ${dir}
                    docker build -t ${imagename}:latest .
                    exit
                    EOF
                    """
                    }
               }
         }

         stage('Image Push') {
            steps {
                sshagent([cred]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    mkdir ${dir}
                    cd ${dir}
                    docker tag ${imagename}:latest angellaviory/dumbmerchbee:latest
                    docker push angellaviory/dumbmerchbee:latest
                    exit
                    EOF
                    """
                    }

