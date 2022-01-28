pipeline {
  agent any
 
  tools {
  maven 'Maven3'
  }
  stages {
    stage ('Checkout') {
      steps {
      git branch: 'stage', credentialsId: 'Github_username', url: 'https://github.com/vams-cmd/maven-helloworld.git'
      }
    }  
    stage ('Build') {
      steps {
      sh 'mvn clean install -f pom.xml'
      }
    }
    stage ('Code Quality') {
      steps {
          withSonarQubeEnv('SonarQube') {
          sh 'mvn -f pom.xml sonar:sonar'
          }
      }
    }
	
    stage ('Build Dockerimage') {
        agent {
        label 'jenkins-slave1'
        }
        steps {
            sh '''
            cp /home/ubuntu/jenkins/workspace/1st_Assignment_stage/target/my-app-1.0-SNAPSHOT.jar /home/ubuntu/jenkins/workspace/1st_Assignment_stage
            cd /home/ubuntu/jenkins/workspace/1st_Assignment_stage
	    docker rm bvk10r/ct-assignments:1
	    docker rm assignment1:1
            docker build -t assignment1 .
            docker tag assignment1:latest bvk10r/ct-assignments:1 
	    docker run -d --name ass_cont bvk10r/ct-assignments:1
            docker push bvk10r/ct-assignments:1
            '''
        }
    }  
  }
}
