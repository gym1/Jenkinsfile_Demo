
pipeline {
    agent any
    stages{
        stage('Get latest version of code') {
            steps{
                checkout scm
            }
        }
        stage('Build') {
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
                        //junit '**/cobertura.xml'
                    }
                }
            }
        }
        stage('Run Code Coverage') {
            steps{
                echo 'Cannot locate report'
                //cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: '**/cobertura.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
            }
        }
        stage('Deploy Local') {
            steps{
                echo 'Hi'
            }
        }
        stage('Run Integration Tests') {
            steps{
                echo 'Hu'
            }
        }
        stage('Deploy Production') {
            steps{
                echo 'He'
            }
        }
        stage('Run Post Deployment Tests') {
            steps {
                echo 'Pop me an meesage'
            }
        }
    }
}
