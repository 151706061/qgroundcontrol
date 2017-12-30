pipeline {
  agent any
  stages {
    stage('build') {
      parallel {
        stage('Linux') {
          agent {
            docker {
              image 'mavlink/qgc-build-linux'
            }
            
          }
          steps {
            sh '''mkdir build
cd build
qmake ../qgroundcontrol.pro'''
          }
        }
        stage('Android') {
          agent {
            docker {
              image 'mavlink/qgc-build-android'
            }
            
          }
          steps {
            sh '''mkdir build
cd build
qmake ../qgroundcontrol.pro'''
          }
        }
      }
    }
  }
}