// plugins used: docker pipeline
// setup dockerhub credentials in global security credentials


pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('dockercred')
	}

	stages {
	    
	    stage('build') {
	        steps {
	            sh 'git clone https://github.com/adsnjhfyeqw231eas/SLlab-proj2.git'
	            sh 'cd SLlab-proj2 && ls && docker build -t tguha-nginx .'
	            sh 'docker image ls'
	        }
	    }
		stage('Tag') {
			steps {
				sh 'docker tag tguha-nginx tridevg/nginx-june:v1'
			}
		}
		stage('Login') {
			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}
		stage('Push') {
			steps {
				sh 'docker push tridevg/nginx-june:v1'
			}
		}
// 		stage('Cleanup') {
// 		    steps {
// 		        sh 'docker rmi tguha-nginx:latest'
// 		        sh 'docker rmi ubuntu:latest'
// 		        sh 'docker rmi tridevg/nginx-june:v1'
// 		        sh 'dokcer images'
// 		    }
// 		}

	// Continous Delivery approval
        stage('Approve Delivery of app?') {
            steps {
                input('Do you want to proceed?')
            }
        }
        stage('App Continuous Delivery Approved') {
            steps {
                sh 'docker run -d -p 80:80 --name=project2-nginx tridevg/nginx-june:v1'
            }
        }
		
	}

}



