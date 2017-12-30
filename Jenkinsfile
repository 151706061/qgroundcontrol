pipeline {
  agent any
  stages {
    stage('build') {
      parallel {
        stage('Linux Release') {
          agent {
            docker {
              image 'mavlink/qgc-build-linux'
            }
            
          }
          steps {
            sh '''git submodule update --init --recursive
rm -rf build; mkdir build; cd build
qmake -r ../qgroundcontrol.pro CONFIG+=installer CONFIG+=WarningsAsErrorsOn'''
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
        stage('Linux Debug') {
          agent {
            docker {
              image 'mavlink/qgc-build-linux'
            }
            
          }
          steps {
            sh '''git submodule update --init --recursive
rm -rf build; mkdir build; cd build
qmake -r ../qgroundcontrol.pro CONFIG+=debug CONFIG+=WarningsAsErrorsOn'''
            sh './debug/qgroundcontrol-start.sh --unittest'
          }
        }
      }
    }
  }
}