pipeline {
  agent none

  stages {
    stage('worker build') {
      agent {
        docker {
          image 'maven:3.6.1-jdk-8-alpine'
          args '-v $HOME/.m2:/root/.m2'
        }
      }
      steps {
        echo 'Compiling worker app'
        dir('worker'){
          sh 'mvn compile'
        }
      }
    }
    stage('worker test') {
      agent {
        docker {
          image 'maven:3.6.1-jdk-8-alpine'
          args '-v $HOME/.m2:/root/.m2'
        }
      }
      steps {
        echo 'Unit Tests of worker app'
        dir('worker'){
          sh 'mvn clean test'
        }
      }
    }
    stage('worker package') {
      agent {
        docker {
          image 'maven:3.6.1-jdk-8-alpine'
          args '-v $HOME/.m2:/root/.m2'
        }
      }
      steps {
        echo 'Packaging worker app'
        dir('worker'){
          sh 'mvn package -DskipTests'
        }
      }
    }
//    stage('worker docker-package') {
//      agent any
//      steps {
//        echo "Packaging and publishing image"
//        script {
//          docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
//            def workerImage = docker.build("speeldight/worker:v${env.BUILD_ID}", "./worker")
//            workerImage.push()
//          }
//        }
//      }
//    }
    stage('vote build') {
      agent {
        docker {
          image 'python:2.7.16-slim'
          args '--user root'
        }
      }
      steps {
        echo 'Compiling vote app'
        dir('vote'){
          sh 'pip install -r requirements.txt'
        }
      }
    }
    stage('vote test') {
      agent {
        docker {
          image 'python:2.7.16-slim'
          args '--user root'
        }
      }
      steps {
        echo 'Unit Tests of vote app'
        dir('vote'){
          sh 'pip install -r requirements.txt'
          sh 'nosetests -v'
        }
      }
    }
//    stage('vote docker-package') {
//      agent any
//      steps {
//        echo "Packaging and publishing image"
//        script {
//          docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
//            def workerImage = docker.build("speeldight/vote:v${env.BUILD_ID}", "./vote")
//            workerImage.push()
//          }
//        }
//      }
//    }
  }
}
