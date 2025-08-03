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
    sshagent(['tomcat-key']) {
      sh '''
       scp -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null \
-i /var/lib/jenkins/.ssh/key.pem \
/var/lib/jenkins/workspace/maven-deploy/target/idream-it-solutions.war \
ubuntu@172.31.89.126:/home/ubuntu/tomcat9/webapps/
      '''
    }
  }
}
  }
}
