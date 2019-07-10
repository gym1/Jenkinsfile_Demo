
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
        // compile parallel
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
                	parallel{
                		stage('PC Compile'){
                			steps{
                				echo 'Compile to a bin file'
                				sh 'gcc -Wall Reverse_String_I.c -o stringR.bin'
                			}
                		}
                		stage('Lunix Compile'){
                			steps{
                				echo 'Compile to a bin file'
                				sh 'gcc -Wall Reverse_String_I.c -o stringR.bin'
                			}
                		}
                		stage('Special Compile'){
                			steps{
                				echo 'Compile to a bin file'
                				sh 'gcc -Wall Reverse_String_I.c -o stringR.bin'
                			}
                		}                  
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
        	agent{
        		docker { image 'node:7-alpine' }
        	}
            stages{
                stage('Smoke Test'){
                    steps{
                        echo 'Doing Quick QA Test with Zone Control'
                        //sh './stringR.bin'
                    }
                }
                stage('Unit Test'){
                    steps {
                        echo 'Full QA Testing with zone control'
                        //sh './stringR.bin'
                        //junit 'build/**/*.xml'
                        //junit '**/cobertura.xml'
                    }
                }
                stage('Run Code Coverage') {
                    steps{
                        echo 'Generate code Coverage'
                        archive '/var/lib/jenkins/workspace/Jenkins_Demo1/stringR.bin'
                        publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: '', reportFiles: 'htmlpublisher-wrapper.html', reportName: 'Code Coverage', reportTitles: 'Show Something'])
                        //cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: '**/cobertura.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
                    }
                }
                stage('Automation Test'){
                    steps{
                        echo 'Run inifinite Test'
                    }
                }
            }
            ///post {
                //always {
                    //junit 'build/reports/**/*.xml'
                //}
            //}
        }
        stage('Deploy Local Stage') {
            stages{
                stage('Analysis Result'){
                    steps{
                        echo 'Setup a standard'
                    }
                }
                stage('Push the Container'){
                    steps{
                        echo 'run pre-intergration test'
                    }
                }
            }
        }
        stage('Run Integration Tests') {
            stages{              
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
