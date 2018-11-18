pipeline {
  agent { label 'linux' }

  stages {
    stage ('Unit Tests'){ 
      steps {   
        sh "ant"
        sh "ant -f test.xml -v"
        sh "junit 'reports/result.xml'"
      }
    }
  }
}
