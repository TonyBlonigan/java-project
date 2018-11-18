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
        sh "pwd"
      }
    }
    stage ('Deploy'){
      steps {
        sh "aws s3 cp dist/rectangle-${BUILD_NUMBER}.jar s3://jenkins-java/rectangle.jar"
      }
    }
  }
}
