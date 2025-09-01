# Jenkins CI/CD Pipeline - Node.js Demo

This project demonstrates a simple Jenkins pipeline for a Node.js application using Docker.

---

## 📁 Project Structure

.
├── Jenkinsfile
├── Nodejs_App
│ ├── package.json
│ └── (build + test files go here)
└── README.md

yaml
Copy code

---

## 🚀 Overview

This pipeline is configured to:

1. **Use Docker** with a Node.js 16 Alpine image.
2. **Check out** the source code from the SCM (e.g., Git).
3. **Install dependencies**, run tests, and build the app inside the `Nodejs_App` directory.
4. **Archive the built artifacts** from the `dist/` directory for further use (e.g., deployment or download).

---

## 🛠 Jenkinsfile Details

```groovy
pipeline {
    agent none

    stages {
        stage('Checkout and Build') {
            agent {
                docker {
                    image 'node:16-alpine'
                }
            }
            options {
                skipDefaultCheckout()
            }
            steps {
                checkout scm

                dir('Nodejs_App') {
                    sh 'ls -la'           // Verify files
                    sh 'npm install'     // Install packages
                    sh 'npm test'        // Run tests
                    sh 'npm run build'   // Build project
                }
            }
            post {
                success {
                    archiveArtifacts artifacts: 'Nodejs_App/dist/**', fingerprint: true
                }
            }
        }
    }
}
📦 package.json
Here's the minimal package.json used for this pipeline:

json
Copy code
{
  "name": "jenkins-demo",
  "version": "1.0.0",
  "scripts": {
    "test": "echo 'Running test...' && exit 0",
    "build": "echo 'Building app...' && mkdir -p dist && echo 'Hello Jenkins' > dist/index.html"
  }
}
test: Simulates a passing test.

build: Creates a dist folder with a sample HTML file.

🧪 Requirements
Jenkins with Docker support.

Node.js project located in Nodejs_App/.

Jenkinsfile at the root of the repository.

📦 Build Output
After a successful build, Jenkins archives:

bash
Copy code
Nodejs_App/dist/index.html
You can view or download it from the Jenkins UI.

📌 Notes
The use of agent none at the top disables a global agent — each stage must define its own agent.

skipDefaultCheckout() ensures that the code checkout only happens in the specified stage, avoiding redundancy.

You can expand this setup to include linting, deployment, or notifications.

📤 Example Run Output
bash
Copy code
$ npm install
$ npm test
Running test...

$ npm run build
Building app...
Hello Jenkins
