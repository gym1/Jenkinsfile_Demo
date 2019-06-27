
pipeline {
    agent any
    stages{
        stage('Get latest version of code') {
            steps{
                checkout scm
            }
        }
        // Build and Package Stage will push bin file to backend server
        // and load the bin file into the Safe
        stage('First Build Stage') {
            stages {
                stage('Check GCC'){
                	steps{
                		echo 'check Compiler version'
                	}
                }
                stage('Install Library'){
                	steps{
                		echo 'include enough Library files in the compile file or c file'
                	}
                }
                stage('Compile'){
                	steps{
                		echo 'Compile to a bin file'
                		sh 'gcc -Wall Reverse_String_I.c -o stringR.bin'
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
                        sh './stringR.bin'
                    }
                }
                stage('Unit Test'){
                    steps {
                        echo 'QA Testing..'
                        sh './stringR.bin'
                        junit 'build/**/*.xml'
                        //junit '**/cobertura.xml'
                    }
                }
                stage('Run Code Coverage') {
                    steps{
                        echo 'Generate code Coverage'
                        cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: '**/cobertura.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
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
        stage('Run Integration Tests (Container)') {
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
        stage('Deploy Production Stage') {
            stages{
                stage('Analysis Result'){
                    steps{
                        echo 'Setup a standard'
                        sh './stringR > temp.txt'
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


// For Pushing into Git
// Throw an error without explaination
/*
echo 'Pushing'
withCredentials([usernamePassword(credentialsId: 'gym1', passwordVariable: 'lawrence0217', usernameVariable: 'gym1')]) {
sh 'git tag -78987 -m "Jenkins"'
sh 'git push https://${gym1}:${lawrence0217}@<Jenkinsfile_Demo> --tags'
}

*/
