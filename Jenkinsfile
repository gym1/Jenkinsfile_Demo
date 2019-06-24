pipeline { 
    node ('jenkins-pipeline') {
      stage('Get latest version of code') {
        checkout scm
      }

      container ('chrome') {
        stage('Install Packages') {
          sh 'npm install --quiet'
        }

        stage('Code Formatting checks') {
          sh 'npm run lint'
        }

        stage('Build') {
          sh 'npm run build'
        }

        stage('Run Unit Tests') {
          sh 'npm run test-ci'
          junit 'test-results/**/*.xml'
        }
      } //end container chrome

      stage('Run Code Coverage') {
        cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: '**/cobertura.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
      }

      stage('Deploy Local') {
      }
      stage('Run Integration Tests') {
      }
      stage('Deploy Production') {
      }
      stage('Run Post Deployment Tests') {
      }
    } // end node
} // end timestamps
