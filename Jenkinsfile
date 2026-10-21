pipeline {
  agent any
  stages {
    stage('SAST - Semgrep') {
      steps {
        sh '''
          docker run --rm -v "$WORKSPACE:/src" semgrep/semgrep \
            semgrep scan --config auto /src --json --output /src/semgrep-report.json || true
          docker run --rm -v "$WORKSPACE:/src" semgrep/semgrep \
            semgrep scan --config auto /src --severity ERROR --error
        '''
      }
    }
  }
  post {
    always {
      archiveArtifacts artifacts: 'semgrep-report.json', allowEmptyArchive: true
    }
  }
}
