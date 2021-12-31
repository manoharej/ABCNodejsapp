pipeline {
    environment {
      CONTAINER_TEST_IMAGE=  "manohar21/docker_automation"
      dockerImage = ''
    }

    agent any
    stages {
            stage('Cloning our Git') {
                steps {
                git 'https://github.com/manoharej/ABCNodejsapp.git'
                }
            }
			
	    stage('Dockerhub login') {
		    steps {
			    sh 'docker login -u $dockerhub_USER -p $dockerhub_PASSWORD $CI_REGISTRY'
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
