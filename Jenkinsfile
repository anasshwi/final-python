pipeline {
  agent {
    node {
      label 'docker'
    }

  }
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/anasshwi/final-python', branch: 'main', changelog: true, poll: true)
      }
    }

    stage('build') {
      steps {
        sh 'docker build -t finPy:$BUILD_ID .'
      }
    }

    stage('run & test') {
      steps {
        sh 'docker run -itd -p 5000:5000 --name finPy finPy:$BUILD_ID'
        sleep 3
        sh 'curl localhost:5000'
        sh 'docker stop finPy && docker rm finPy'
      }
    }

    stage('push') {
      steps {
        sh 'docker tag finPy:$BUILD_ID anasshwi/final-python:$BUILD_ID'
        sh 'docker login -u anasshwi -p Anas123456'
        sh 'docker push anasshwi/final-python:$BUILD_ID'
      }
    }

  }
}