@Library("Shared") _
pipeline {

    agent { label "raj" }

    stages {
        stage("hello") {
            steps{
                script{
                    hello()
                }
            }
        }
        stage("Code") {
            steps {
                script{
                    clone("https://github.com/Rajankumar69/django-notes-app1.git", "main")
                }
            }
        }

        stage("Build") {
        steps {
            script {
                docker_build(
                    imageName: "django_app",
                    imageTag: "latest"
                    )
                }
            }
        }

        stage("Test") {
            steps {
                echo "This is testing the code"
                echo "done testing"
            }
        }

        stage("Push To DockerHub") {
        steps {
            script {
                docker_push(
                    imageName: "django_app",
                    imageTag: "latest",
                    dockerHubUser: "rajan69106"
                    )
            }
        }
    }
    

        stage("Deploy") {
            steps {
                sh '''
                whoami
                docker compose down || true
                docker compose up -d
                docker ps
                '''
                echo "Done Deployment"
            }
        }
    }
}
