properties([
  pipelineTriggers([pollSCM('H/2 * * * *')])
])

node {
  docker.image('python:2-alpine').inside {
    try {
      stage('Build') {
        sh 'python -m py_compile sources/add2vals.py sources/calc.py'
      }

      stage('Test') {
        sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
      }
    } catch (Exception e) {
      currentBuild.result = 'FAILURE'
      throw e
    }
  }
}
