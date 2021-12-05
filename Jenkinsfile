pipeline {
    agent {
        docker {
            image 'maven:3.6.1-jdk-8-alpine'
            args '-v $HOME/.m2:/root/.m2'
        }
    }

    stages {
        stage('worker build') {
            steps {
                echo 'Compiling worker app'
                dir('worker'){
                  sh 'mvn compile'
                }
            }
        }
        stage('worker test') {
            steps {
                echo 'Unit Tests of worker app'
                dir('worker'){
                  sh 'mvn clean test'
                }
            }
        }
        stage('worker package') {
            steps {
                echo 'Packaging worker app'
                dir('worker'){
                  sh 'mvn package -DskipTests'
                }
            }
        }
    }
    post {
      always {
        archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
        echo 'Pipeline completed'
      }
    }
}
