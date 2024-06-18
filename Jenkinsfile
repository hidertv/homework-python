pipeline {
  agent {
    node {
      label 'ubuntuserver'
    }

  }
  stages {
    stage('build') {
      steps {
        sh 'pip install -r requirements.txt'
        sh 'python db.py -a'
      }
    }

    stage('run') {
      steps {
        sh 'timeout 30s python app.py --host localhost --port 5000 &'
      }
    }

    stage('test') {
      agent any
      steps {
        sh 'curl localhost:5000/api/products > test'
        sh 'cat ./test'
      }
    }

  }
}