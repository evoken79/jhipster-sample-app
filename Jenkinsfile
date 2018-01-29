pipeline {
  agent any
  stages {
    stage('Build') {
      agent{
        docker{
          image 'maven:3-alpine'
          args '-v m2dep:/root/.m2'
        }
      }

      steps{ 
        sh 'mvn -B -DskipTests clean package'
        stash name: 'war',includes: 'target/**'
      }
    }
    stage('Backend') {
      parallel {
        stage('Unit') {
          steps {
            sh 'echo Unit'
          }
        }
        stage('Performance') {
          steps {
            sh 'echo Performance'
          }
        }
      }
    }
    stage('Frontend') {
      steps {
        sh 'echo frontend'
      }
    }
    stage('Static Analysis') {
      steps {
        sh 'echo static'
      }
    }
    stage('Deploy') {
      steps {
        sh 'echo Deploy'
      }
    }
  }
}