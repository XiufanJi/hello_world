pipeline {
  agent any
  stages {
    stage('clone codes') {
      steps {
        git(url: 'https://github.com/XiufanJi/hello_world.git', branch: 'master', changelog: true)
      }
    }

    stage('test') {
      steps {
        sh 'echo "begin test procedure"'
      }
    }

    stage('package') {
      steps {
        archiveArtifacts(onlyIfSuccessful: true, fingerprint: true, artifacts: 'jar')
      }
    }

  }
}