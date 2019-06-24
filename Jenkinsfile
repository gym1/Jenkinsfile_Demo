
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
            parallel{
                stage('Smoke Test'){
                    agent { label "Smoke Test" }
                    steps{
                        echo 'Smoke Testing'
                        sh './stringR'
                    }
                }
                stage('Sanity Test'){
                    agent { label "Sanity Test" }
                    steps {
                        echo 'Testing..'
                        sh './stringR'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Pop me an meesage'
            }
        }
    }
}
