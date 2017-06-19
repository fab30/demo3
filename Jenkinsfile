pipeline {
  agent {
    docker {
      image 'maven:alpine'
    }
    
  }
  stages {
    stage('Build') {
      steps {
        sh 'mvn compile'
      }
    }
    stage('TU') {
      steps {
        parallel(
          "TU": {
            sh 'mvn test'
            junit 'build/**/*.xml'
            
          },
          "TF": {
            node(label: '*') {
              sleep 10
            }
            
            
          },
          "TI": {
            node(label: '*') {
              sleep 20
            }
            
            
          }
        )
      }
    }
    stage('MEP ?') {
      steps {
        input(message: 'Voulez vous mettre en production', id: 'mep', ok: 'Go')
      }
    }
    stage('MEP') {
      steps {
        echo 'En production !'
      }
    }
  }
}