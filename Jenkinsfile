
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script{
                    stage('Check GCC'){                       
                        sh 'gcc -v'
                        sh 'docker version'
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
        @Library('github.com/spotify/jenkins-coverage-poster@1.0') _
        stage("Run tests") {
            sh "mvn test"
        }
        stage("Post coverage") {
            postJacocoCoverage(threshold: 75)
        }
        stage('Deploy') {
            steps {
                echo 'Pop me an meesage'
            }
        }
    }
}
