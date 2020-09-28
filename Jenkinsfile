pipeline{
    agent any
    environment{
				
				Tag = 'snapshot'
				VERSION = "${BUILD_ID}"//docker image version for develope branch
				IMAGE_NAME = 'test-scanning'
                NAME='alpine:3.7'				
    }
    stages{
	
        stage('Docker Build'){
            steps{
				// Build the docker image using a Dockerfile
				sh "docker build . -t ${IMAGE_NAME}:${VERSION}"
                sh "docker pull $NAME"
            }
        }
        stage('Docker Image Scanning'){
            steps{
                echo "***********Scanning Docker Images**********"
				//writeFile file: 'anchore_images', text: "${IMAGE_NAME}:${VERSION} ${WORKSPACE}/Dockerfile"
                //anchore name: 'anchore_images'
                writeFile file: 'anchore_images', text: "${NAME}"
                anchore name: 'anchore_images'
            }
        }					
	}
}