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

### Adding Github WebHook:
1. firstly make git hub token and make credentials on jenkins
2. then you need to create an one projet repo whic consist the "Jenkinsfile" this named file inside that you can write the pipeline cod ewhat you want
3. after that you need to go on that repo settings you will found the webhook option so select it and then continue where you need to enter the url so enter you jenkins server url with ending /github-webhook/ and select not declractive somthing option is there save the changes
4. now come on the jenkins server create new pipeline job where you find some option choose "itHub hook trigger for GITScm polling" then in pieline defintion add "pipeline script fron scm" add there some detail of repo url name etc. and simply save
5. after that build at only starting then you noot need to build it again it automatically triggered when changes occurs.
