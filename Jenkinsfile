node {
  stage('Checkout') {
    checkout scm
  }
  stage('Build') {
    docker.image('python:2-alpine').inside {
      sh 'ls -al sources'
      sh 'python -m py_compile sources/add2vals.py sources/calc.py'
    }
  }
  stage('Test') {
    docker.image('qnib/pytest').inside {
      sh 'pytest --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
      junit 'test-reports/results.xml'
    }
  }
}
