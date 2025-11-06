pipeline {
  agent none 

  triggers {
    pollSCM('* * * * *')
  }


  stages {
    stage('Checkout') {
      agent any
      steps {
        git branch: 'main',
        url: 'https://github.com/j2lee-ko/source-maven-java-spring-hello-webapp.git'
      }
    }
    stage('Build') {
      agent {
        docker { image 'maven:3-openjdk-17' }
      }
      steps {
        sh 'mvn clean package'
      }
    }
    stage('Image Build') {
      agent any
      steps {
        sh 'docker image build -t tomcat:hello .'
      }
    }
    stage('Deploy') {
     agent any
     steps {
       ansiblePlaybook(playbook: 'playbook.yml')
     }
    }
  }
}

