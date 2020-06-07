pipeline {
  agent any
  stages {
    stage('clone codes') {
      steps {
        git(url: 'https://github.com/XiufanJi/hello_world.git', branch: 'master')
      }
    }

    stage('test') {
      steps {
        sh '''#!/bin/bash
echo "begin test!"
mvn package'''
      }
    }

    stage('results') {
      steps {
        archiveArtifacts 'target/*.jar'
      }
    }

  }
}