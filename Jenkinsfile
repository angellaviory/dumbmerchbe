def branch = "main"
def repo = "https://github.com/angellaviory/dumbmerchbe"
def cred = "ubuntu"
def dir = "~/dumbmerchbe"
def server = "192.168.64.49"
def imagename = "dumbmerchbe"

pipeline {
    agent any
    stages {
        stage('Repository pull') {
            steps {
                sshagent([cred]) {
                    sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                    mkdir ${dir}
                    cd ${dir}
                    git init
                    git remote add origin ${repo}
                    git pull origin master
                    git branch ${branch}
                    git checkout ${branch}
                    git pull origin ${branch}
                    exit
                    EOF
                    """
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

