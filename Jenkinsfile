pipeline {
    environment {
      CONTAINER_TEST_IMAGE=  "manohar21/docker_automation"
      CONTAINER_RELEASE_IMAGE= $CI_REGISTRY_IMAGE:latest
      dockerImage = ''
    }

    agent any
    stages {
            stage('Cloning our Git') {
                steps {
                git 'git@github.com:naistangz/Docker_Jenkins_Pipeline.git'
                }
            }
			
			stage('Dockerhub login') {
                steps {
					      sh 'docker login -u $CI_REGISTRY_USER -p $CI_REGISTRY_PASSWORD $CI_REGISTRY'
                }
            }
			
			stage('Docker Build') {
                steps {
                sh 'docker build -t $CONTAINER_TEST_IMAGE .'
                sh 'docker push $CONTAINER_TEST_IMAGE'
                 }
            }

        stage('Docker run') {
            steps {
                sh 'docker run -d -p 3000:3000 $CONTAINER_TEST_IMAGE"
            }
        }

			stage('Cleaning Up') {
                steps{
                  sh "docker rmi --force $CONTAINER_RELEASE_IMAGE"
                }
            }
        }
    }
