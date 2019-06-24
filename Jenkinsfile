
pipeline {
    agent any
    stages {
        stage('Build') {
            stage('Check GCC'){
                steps {
                    sh 'gcc -v'
                    sh 'echo "Hello World"'
                }
            }
            stage('GCC Compile'){
                steps {
                    sh 'gcc -Wall Reverse_String_I.c -o stringR'
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
