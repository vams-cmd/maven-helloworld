pipeline {
  agent any
 
  tools {
  maven 'Maven3'
  }
  stages {
    stage ('Checkout') {
      steps {
      git branch: 'Dev', credentialsId: 'Github_username', url: 'https://github.com/vams-cmd/maven-helloworld.git'
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
  }
}
