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
            sh '''git submodule update --init --recursive
rm -rf build; mkdir build; cd build
qmake -r ../qgroundcontrol.pro'''
          }
        }
        stage('Android') {
          agent {
            docker {
              image 'mavlink/qgc-build-android'
            }
            
          }
          steps {
            sh '''git submodule update --init --recursive
rm -rf build; mkdir build; cd build
qmake -r ../qgroundcontrol.pro'''
          }
        }
      }
    }
  }
}