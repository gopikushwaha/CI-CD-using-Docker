pipeline {
    agent any
	
tools
    {
       maven "maven"
    }
// 	environment{
// 		dockerhub_passwd=credentials('dockerhub')
// 	}
 stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/gopikushwaha/CI-CD-using-Docker.git'
             
          }
        }
	 stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }

  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t simple_mvn_docker:latest .' 
                sh 'docker tag simple_mvn_docker gopikushwaha/simple_mvn_docker:latest'
                //sh 'docker tag simple_mvn_docker gopikushwaha/simple_mvn_docker:$BUILD_NUMBER'
               
          }
        }
  stage('Publish image to Docker Hub') {
          
            steps {
// 		    withDockerRegistry([ credentialsId: "dockerhub", url: "https://index.docker.io/v1/" ]) {
//  	  sh 'docker login -u gopikushwaha -p "gopi69$@#"'
//           sh  'docker push gopikushwaha/simple_mvn_docker:latest'
//         }
// 	      sh 'echo $dockerhub_passwd | docker login -u gopikushwaha --password-stdin'
              sh 'docker push gopikushwaha/simple_mvn_docker:latest'    
          }
        } 
 
      stage('Run Docker container on Jenkins Agent') {
             
            steps 
			{
                sh "docker run -d -p 8003:8080 gopikushwaha/simple_mvn_docker"
 
            }
        }
 }}
//  stage('Run Docker container on remote hosts') {
             
//             steps {
//                 sh "docker -H ssh://jenkins@172.31.28.25 run -d -p 8003:8080 nikhilnidhi/samplewebapp"
 
//             }
//         }
//     }
// 	}
    
