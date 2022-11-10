pipeline {
  agent {
    label 'slave1'
  }
  environment{
     CODEDIR='/var/lib/jenkins/workspace/webapp-deploy-pipeline'
    }
  stages {
    stage('get the code from s3') {
      steps {
        dir("${env.CODEDIR}") {
        echo 'Building the code with maven'
        sh '''
        aws s3 cp s3://mywebapp-code/mywebapp-"$version".war .
        '''
        }
      }
    }
    stage('deploy') {
      steps {
        dir("${env.CODEDIR}") {
        echo 'Deploying the code in tomcat'
        sh '''
        scp /var/lib/jenkins/workspace/webapp-deploy-pipeline/mywebapp-"$version".war root@10.0.1.112:/opt/tomcat9/webapps/mywebapp.war
        '''
        }
      }
    }
  }
}
