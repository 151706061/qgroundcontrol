pipeline {
  agent any
  stages {
    stage('build') {
      parallel {
        stage('Linux Release') {
          agent {
            docker {
              image 'mavlink/qgc-build-linux'
              args '-e CCACHE_BASEDIR=$WORKSPACE -e CCACHE_DIR=/tmp/ccache -v /tmp/ccache:/tmp/ccache:rw'
            }
            
          }
          steps {
            sh 'git submodule update --init --recursive'
            sh 'rm -rf build; mkdir build'
            sh 'ccache -z'
            sh 'cd build && qmake -r ../qgroundcontrol.pro CONFIG+=installer CONFIG+=WarningsAsErrorsOn'
            sh 'cd build && make -j4'
            sh 'ccache -s'
          }
        }
        stage('Android') {
          agent {
            docker {
              image 'mavlink/qgc-build-android:2017-12-29'
              args '-e CCACHE_BASEDIR=$WORKSPACE -e CCACHE_DIR=/tmp/ccache -v /tmp/ccache:/tmp/ccache:rw'
            }
            
          }
          steps {
            sh 'git submodule update --init --recursive'
            sh 'rm -rf build; mkdir build'
            sh 'ccache -z'
            sh 'cd build && qmake -r ../qgroundcontrol.pro'
            sh 'cd build && make -j4'
            sh 'ccache -s'
          }
        }
        stage('Linux Debug') {
          agent {
            docker {
              image 'mavlink/qgc-build-linux'
              args '-e CCACHE_BASEDIR=$WORKSPACE -e CCACHE_DIR=/tmp/ccache -v /tmp/ccache:/tmp/ccache:rw'
            }
            
          }
          steps {
            sh 'git submodule update --init --recursive'
            sh 'rm -rf build; mkdir build'
            sh 'ccache -z'
            sh 'cd build && qmake -r ../qgroundcontrol.pro CONFIG+=debug CONFIG+=WarningsAsErrorsOn'
            sh 'cd build && make -j4'
            sh 'ccache -s'
            sh 'cd build && ./debug/qgroundcontrol-start.sh --unittest'
          }
        }
      }
    }
  }
}
