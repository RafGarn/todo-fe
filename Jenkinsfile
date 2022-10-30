pipeline {
    agent any
    environment {     
    DOCKERHUB_CRE=credentials('dockerhub credentials')
    } 
    stages {
        stage('Build') {
            steps {
                sh "echo 'This is a build step'"
                sh "DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipeline -t rafaelagar/todo-fe:jenkins-${env.BUILD_ID} --target BUILD ."
            }
        }
        stage('Test') {
            steps {
                sh "echo 'This is a test stage'"
            	sh "DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipeline -t rafaelagar/todo-fe:jenkins-${env.BUILD_ID} --target TEST ."

            }
        }
        stage('Delivery artifact') {
            steps {
                sh "DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipeline -t rafaelagar/todo-fe:jenkins-${env.BUILD_ID} --target DELIVERY ."
            }
        }
        stage('Cleanup') {
            steps {
            	sh 'docker system prune'
            }
        }    


        stage('Push') {
            steps {
            	sh "echo 'tagging image as latest'"
                sh "docker image tag rafaelagar/todo-fe:jenkins-${env.BUILD_ID} rafaelagar/todo-fe:latest"
                sh "echo 'Pushing image to dockerhub'"
                sh "sudo docker login -u ${DOCKERHUB_CRE} -p ${DOCKERHUB_CRE_PSW}"
                sh 'sudo docker image push --all-tags rafaelagar/todo-fe'
                sh 'docker logout' 
            }
        }
    }
}
