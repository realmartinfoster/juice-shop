pipeline {
  agent any
  stages {
    stage('SAST - Semgrep') {
      steps {
        sh '''
          docker run --rm -v jenkins_home:/var/jenkins_home -w /var/jenkins_home/workspace/juice-shop-pipeline \
            semgrep/semgrep semgrep scan --config auto . --json --output semgrep-report.json || true
          docker run --rm -v jenkins_home:/var/jenkins_home -w /var/jenkins_home/workspace/juice-shop-pipeline \
            semgrep/semgrep semgrep scan --config auto . --severity ERROR --error
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
