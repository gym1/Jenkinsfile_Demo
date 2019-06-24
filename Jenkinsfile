
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script{
                    stage('Check GCC'){                       
                        sh 'gcc -v'
                        sh 'echo "Hello World"'
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
                    }
                }
            }
        }
        stage('Running the tests with PHPunit'){
            sh 'docker run -v /var/coverage/reportsr:/var/www/reports composer tests'
        }
        stage('Generating test coverage'){
            step([
                $class: 'CloverPublisher',
                cloverReportDir: '/var/coverage/reports/',
                cloverReportFileName: 'coverage.xml',
                healthyTarget: [methodCoverage: 70, conditionalCoverage: 80, statementCoverage: 80],
                unhealthyTarget: [methodCoverage: 50, conditionalCoverage: 50, statementCoverage: 50],
                failingTarget: [methodCoverage: 0, conditionalCoverage: 0, statementCoverage: 0]
            ])
        }
        stage('Deploy') {
            steps {
                echo 'Pop me an meesage'
            }
        }
    }
}
