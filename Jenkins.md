### Pipeline Job:
### Pull/ make clone the private repo to the jenkins server:
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
4. after that build the changes.
5. and your pipeline worked!!!!

---

### Making Clone of git repo, Docker images installation, DockerHub login, Push the docker image into docker account:
1. make credentials for docker hub account login by username and password i.e PAT
2. install docker on jenkins server and make sure it work or not if not then give permission( sudo usermod -aG docker jenkins, newgrp jenkins)
3. then comes on pipeline and write the code
---
pipeline {

    agent any
    
    environment {
        IMAGE_NAME = "bhavanaghule/new-nginx"
        IMAGE_TAG = "latest"
    }
    stages {
        stage('Clone') {
            steps {
                echo "Cloning project from GitHub to Jenkins server"
                git branch: 'main',
                    credentialsId: 'github-token',
                    url: 'https://github.com/Bhavana-Ghule/DevOps-notes.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
            }
        }

        stage('Docker Hub Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-token',
                    usernameVariable: 'DOCKER_USERNAME',
                    passwordVariable: 'DOCKER_PASSWORD'
                )]) {
                    sh '''
                        echo "$DOCKER_PASSWORD" | docker login \
                        -u "$DOCKER_USERNAME" \
                        --password-stdin
                    '''
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
            }
        }
    }
}
----
4. after that build changes and look in server as well as docker hub you will find the docker image will install!!!
