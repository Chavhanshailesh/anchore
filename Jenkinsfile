pipeline{
    agent any
    environment{
        VERSION = "${BUILD_ID}"//docker image version for develope branch
        NAME='alpine:3.7'				
    }
    stages{
        stage('Docker Build'){
            steps{
				//Build the docker image using a Dockerfile
                sh "docker pull $NAME"
            }
        }
        stage('Docker Image Scanning'){
            steps{
                echo "***********Scanning Docker Images**********"
                writeFile file: 'anchore_images', text: "${NAME}"
                anchore name: 'anchore_images'
            }
        }			
	}
}