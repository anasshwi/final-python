pipeline {
  agent {
    node {
      label 'dicker'
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
        sh 'docker build -t final-python:$BUILD_ID .'
      }
    }

    stage('run & test') {
      steps {
        sh 'docker run --name final-python -d -p 5000:5000 final-python:$BUILD_ID'
        sleep 3
        sh 'curl localhost:5000'
        sh 'docker stop final-python && docker rm final-python'
      }
    }

    stage('push') {
      steps {
        sh 'docker tag final-python:$BUILD_ID anasshwi/final-python:$BUILD_ID'
        sh 'docker login -u anasshwi -p Anas123456'
        sh 'docker push anasshwi/final-python:$BUILD_ID'
      }
    }

  }
}