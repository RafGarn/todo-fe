pipeline {
    agent any
    environment {     
    DOCKERHUB_CRE=credentials('dockerhub credentials')
    } 
    stages {
        stage('Build') {
            steps {
                sh "DOCKER_BUILDKIT=1 docker build -t rafaelagar/todo-fe:jenkins-${env.BUILD_ID} -t rafaelagar/todo-fe:latest --target BUILD ."
            }
        }
        stage('Test') {
            steps {
            	sh "DOCKER_BUILDKIT=1 docker build -t rafaelagar/todo-fe:jenkins-${env.BUILD_ID} -t rafaelagar/todo-fe:latest --target TEST ."

            }
        }
        stage('Delivery artifact') {
            steps {
                sh "DOCKER_BUILDKIT=1 docker build -t rafaelagar/todo-fe:jenkins-${env.BUILD_ID} -t rafaelagar/todo-fe:latest --target DELIVERY ."
            }
        }
        stage('Cleanup') {
            steps {
            	sh 'docker system prune'
            }
        }    


        stage('Push') {
            steps {
            	echo 'Pushing image to dockerhub'
                sh 'sudo docker login -u ${DOCKERHUB_CRE} -p ${DOCKERHUB_CRE_PSW}'
                sh 'sudo docker push rafaelagar/todo-fe'
                sh 'docker logout' 
            }
        }
    }
}
