# Jenkins Docker Agent Pipeline

A simple Jenkins pipeline to verify if the Docker agent (slave) configuration is working as expected.

## 📦 Overview

This project demonstrates how to run a Jenkins pipeline inside a Docker container using the `node:16-alpine` image. The pipeline simply prints the Node.js version to validate that:

- Jenkins is correctly set up to run pipelines with Docker agents.
- The Docker container (`node:16-alpine`) is working as expected.

## 🧰 Technologies Used

- Jenkins
- Docker
- Node.js (v16, Alpine-based image)

## ⚙️ Jenkinsfile

Here’s the sample pipeline used:

```groovy
pipeline {
  agent {
    docker { image 'node:16-alpine' }
  }
  stages {
    stage('Test') {
      steps {
        sh 'node --version'
      }
    }
  }
}

# What This Does

1.Pulls the node:16-alpine Docker image.

2.Runs the pipeline in a container based on that image.

3.Executes node --version to verify the Node.js environment inside the container.

# Setup Instructions

1.Make sure Jenkins is installed and running with Docker support.

2.Create a new Pipeline job in Jenkins.

3.Point it to this repository containing the Jenkinsfile.

Run the pipeline — you should see the Node.js version printed in the console output.
