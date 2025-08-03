pipeline {
  agent any

  //environment {
   // MVN_HOME = '/usr/share/maven'
  //}

  stages {
    stage('Clone') {
      steps {
        git url: 'https://github.com/madhumayee/webapp.git'
      }
    }

    stage('Build') {
      steps {
        sh 'mvn clean install'
      }
    }

    stage('Upload to Nexus') {
      steps {
        sh 'mvn deploy'
      }
    }

   stage('Deploy to Tomcat') {
      steps {
        //sshagent(['tomcat-ssh-key']) {
          sh """
          scp /var/lib/jenkins/workspace/maven-deploy/target/*.war ubuntu@172.31.90.28:/home/ubuntu/tomcat9/webapps/
          """
        }
    }
  }
}
