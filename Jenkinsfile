
pipeline{
  agent none
  options {
    timeout(time: 10, unit: 'MINUTES')     
  }
  stages{
  stage('Agent'){
    agent { label 'maven'}
    steps {
      container('maven'){
        echo 'Hello World'
        sh 'java -version'
      }
    }
  }
  stage('Determine Jenkinsfile to build') {
      def sout = sh(returnStdout: true, script: 'git diff --name-only origin/master...HEAD')
      def j = findJenkinsfileToRun(sout.split())

      if (j.toString() == "${pwd()}/Jenkinsfile") {
          println("Building the whole world")

          load "Jenkinsfile-build-the-world"

      } else {
          println("Building ${j.toString()}")
          load "${j.toString()}"
      }
    }
  }
}

