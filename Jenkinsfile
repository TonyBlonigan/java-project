pipeline {
  agent { label 'linux' }

  stages {
    stage ('Unit Tests'){ 
      steps {
        sh "ant -f test.xml -v"
        junit 'reports/*.xml'
      }
    }
    stage ('Build'){
      steps {
        sh "ant -f build.xml -v"
      }
    }
    stage ('Deploy'){
      steps {
        sh "aws s3 cp dist/rectangle-${BUILD_NUMBER}.jar s3://jenkins-java/rectangle-${BUILD_NUMBER}.jar"
      }
    }
    stage ('Report'){
      steps {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'b24893d6-56fc-423b-ace7-c74208c68a79', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
          sh "aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins"
        }
      }
    }
  }
}
