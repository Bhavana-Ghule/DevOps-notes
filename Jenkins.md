### Pipeline Job (for pull the private repo to the jenkins server:
##### steps to be folloe:
1. create the git token with selectecting private repo and give permision (content -read-only)-> generate token
2. create credentials at jenkins management with username and password git username password that you create PAT -> and generate credential
3. write the code of pipeline
---
pipeline {
    agent any
    stages {
        stage('clone'){
            steps{
                echo "cloning project from github to jenkins-server"
                git branch: 'main',
                credentialsId: 'github-token',
                url: 'https://github.com/Bhavana-Ghule/Jenkins.git'
            }
        }
        stage('build'){
            steps{
                echo "building code from dockerfile to docker-image"
                sh 'touch raj'
            }
        }
    }
}
---
4. after that build the changes
