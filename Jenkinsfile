/*
pipeline {
    agent any
    stages{
        stage('Get latest version of code') {
            steps{
                checkout scm
            }
        }
        stage('First Build Stage') {
            steps {
                script{
                    stage('Check GCC'){                       
                        sh 'gcc -v'
                    }
                    stage('Install Package'){
                        sh 'npm install --quiet'
                    }
                    stage('GCC Compile'){
                        sh 'gcc -Wall Reverse_String_I.c -o stringR'
                    }
                }
            }
        }
        stage('Package Stage'){
            stages{
                stage('Push bin to backend'){
                    steps{
                        echo 'Pushing'
                    }
                }
                stage('Load to Safe'){
                    steps{
                        echo 'Loading...'
                    }
                }
            }
        }            
        stage('Test Stage') {
            stages{
                stage('Smoke Test'){
                    steps{
                        echo 'Doing No-Zone QA Test'
                        sh './stringR'
                    }
                }
                stage('Unit Test'){
                    steps {
                        echo 'QA Testing..'
                        sh './stringR'
                    }
                }
                stage('Run Code Coverage') {
                    steps{
                        echo 'Generate code Coverage'
                     
                    }
                }
                stage('Automation'){
                    steps{
                        echo 'Run Full QA_Test'
                    }
                }
            }
        }
        stage('Deploy Local Stage') {
            stages{
                stage('Analysis Result'){
                    steps{
                        echo 'Setup a standard'
                    }
                }
                stage('Merge Code Local'){
                    steps{
                        echo 'Auto Merge Code based on standard'
                    }
                }
            }
        }
        stage('Run Integration Tests (Container') {
            stages{
                stage('Re-Build'){
                    steps{
                        echo 'Re-Building/Compile......'
                    }
                }
                stage('Re-Package'){
                    steps{
                        echo 'Re-Package......'
                    }
                }                
                stage('Sanity Test'){
                    steps{
                        echo 'Re-Do QA_Test'
                    }
                }
                stage('Full Test'){
                    steps{
                        echo 'Run all five tests'
                    }
                }
                stage('Test Report'){
                    steps{
                        echo 'Generate a full test report'
                    }
                }                
            }
        }
        stage('Deploy Production') {
            stages{
                stage('Analysis Result'){
                    steps{
                        echo 'Setup a standard'
                    } 
                }
                stage('Merge Code'){
                    steps{
                        echo 'Merge Code to dev-branch'
                    }
                }
                stage('Release Check'){
                    steps{
                        echo 'Check for release'
                    }
                }
            }
        }
    }
}
*/
/*
node{
	stage('Get latest version of code') {
        checkout scm
    }
    stage('First Build Stage') {
    	stage('Check GCC'){                       
            sh 'gcc -v'
        }
        stage('Install Package'){
            sh 'npm install --quiet'
        }
        stage('GCC Compile'){
            sh 'gcc -Wall Reverse_String_I.c -o stringR'
        }
    }
}
*/

#!/usr/bin/groovy

timestamps { 
  podTemplate(
    label: 'jenkins-pipeline', 
    inheritFrom: 'default',
    containers: [
      containerTemplate(name: 'chrome', image: 'garunski/alpine-chrome:latest', command: 'cat', ttyEnabled: true)
    ]
  ) {
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
  } // end podTemplate
} // end timestamps