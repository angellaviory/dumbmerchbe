def branch = "main"
def remote = "origin"
def dir = "~/dumbmerchfe"
def server = "192.168.64.49"
def credi = "jenkins"

pipeline {
	agent any
	stages {
		stage ('Pull From Git'){
			steps{
				sshagent ([credi]) {
					sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
					cd ${dir}
					git pull ${remote} ${branch}
					exit
					EOF"""
				}
			}
		}
	

                stage ('docker build'){
                        steps{
                                sshagent ([credi]) {
                                        sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                                        cd ${dir}
                                        docker build -t dumbmerch-bee .
                                        exit
                                        EOF"""
                                }
                        }
                }
        

                stage ('docker run'){
                        steps{
                                sshagent ([credi]) {
                                        sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                                        cd ${dir}
                                        docker run -d -p 5000:5000 dumbmerch-bee
                                        exit
                                        EOF"""
                                }
                        }
                }
        
                stage ('docker push'){
                        steps{
                                sshagent ([credi]) {
                                        sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                                        cd ${dir}
					docker tag dumbmerch-bee:latest angellaviory/dumbmerch-bee:latest
                                        docker push angellaviory/dumbmerch-bee:latest
                                        exit
                                        EOF"""
                                }
                        }
                }	
	}
}
