pipeline {
    agent { label "Jenkins-Agent" }
    environment {
              APP_NAME = "register-app-pipeline"
    }

    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }

        stage("Checkout from SCM") {
               steps {
                  git branch: 'main', credentialsId: 'github', url: 'https://github.com/Parthasarathy28/register-app.git'
               }
        }
        stage("Push the changed deployment file to Git") {
            steps {
                sh """
                   git config --global user.name "Parthasarathy28"
                   git config --global user.email "parthasarathi.parandhaman@gmail.com"
                   git add deployment.yaml
                   git commit -m "Updated Deployment Manifest"
                """
                withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
                  sh "git push https://github.com/Parthasarathy28/gitops-register-app.git"
                }
            }
        }

                     
    }
}
