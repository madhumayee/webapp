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
        sshagent(['tomcat-ssh-key']) {
          sh '''
            mkdir -p ~/.ssh
            ssh-keyscan -H 172.31.84.17 >> ~/.ssh/known_hosts
            scp target/*.war ubuntu@172.31.84.17:/home/ubuntu/tomcat9/webapps/
          '''
        }
      }
    }
  }
}
