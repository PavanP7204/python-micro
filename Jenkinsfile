#!/usr/bin/env groovy
pipeline {
    agentany
    environment {
        registry = "docker.io"
        registryCredential = 'dockerhub-credential'
        imageName = "my-image"
        imageTag = "${env.BUILD_NUMBER}"
    }

    stages {
        stage('Build Image') {
            when {
                branch 'https://github.com/PavanP7204/python-micro.git'  //only run these steps on the master branch
            }
            steps {
                script {
                    docker.build("my-image:${env.BUILD_NUMBER}")
                }

            // Jenkins Stage to Build the Docker Image

        }

        stage('Publish Image') {
            when {
                branch 'https://github.com/PavanP7204/python-micro.git'  //only run these steps on the master branch
            }
             steps {
                script {
                    docker.withRegistry( "https://${registry}", registryCredential ) {
                        dockerImage.push()
                    }
                }
            // Jenkins Stage to Publish the Docker Image to Dockerhub or any Docker repository of your choice.

        }
    }
}