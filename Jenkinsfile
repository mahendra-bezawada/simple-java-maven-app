pipeline {
  agent any

  environment {
    CI = true
    ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token')
  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean install'
      }
    }
    stage('Upload to Artifactory') {
      agent {
        docker {
          image 'releases-docker.jfrog.io/jfrog/jfrog-cli-v2:2.2.0' 
          reuseNode true
        }
      }
      steps {
        sh 'jfrog rt upload --url http://54.215.233.239:8082/artifactory/ --access-token ${ARTIFACTORY_ACCESS_TOKEN} target/my-app-1.0-SNAPSHOT.jar java-web-app/'
      }
    }
  }
}