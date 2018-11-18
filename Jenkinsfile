pipeline {
  agent { label 'linux' }

  stages {
    stage ('Unit Tests'){ 
      steps {   
        sh "ant"
        sh "ant -f test.xml -v"
        junit 'reports/*.xml'
      }
    }
    stage ('Build'){
      ant
    }
  }
}
