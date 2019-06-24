
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script{
                    stage('Check GCC'){                       
                        sh 'gcc -v'
                    }
                    stage('GCC Compile'){
                        sh 'gcc -Wall Reverse_String_I.c -o stringR'
                    }
                }
            }            
        }
        stage('Test') {
            stages{
                stage('Smoke Test'){
                    steps{
                        echo 'Smoke Testing'
                        sh './stringR'
                    }
                }
                stage('Sanity Test'){
                    steps {
                        echo 'Testing..'
                        sh './stringR'
                        junit 'test-results/**/*.xml'
                    }
                }
            }
        }
      stage('Run Code Coverage') {
          steps{
            cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: '**/cobertura.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
          }
      }
        stage('Deploy') {
            steps {
                echo 'Pop me an meesage'
            }
        }
    }
}
