pipeline {
  agent any
  stages {
    stage('Fetch and check tags') {
      steps {
        git(url: 'git@github.com:nickoe/kicad-source-mirror.git', branch: 'master')
        git(url: 'git@github.com:nickoe/kicad-doc.git', branch: 'master')
      }
    }
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            build 'osx-kicad-adam-new-head'
            build 'osx-kicad-adam-head'
          }
        }
        stage('') {
          steps {
            build 'linux-kicad-full-gcc-head'
            build 'linux-kicad-full-clang-head'
          }
        }
      }
    }
    stage('') {
      steps {
        warnings(canComputeNew: true, includePattern: 'warning:')
      }
    }
  }
}