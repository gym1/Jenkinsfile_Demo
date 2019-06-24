
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                scripts{
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
            steps {
                echo 'Testing..'
                sh './stringR'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Pop me an meesage'
            }
        }
    }
}
