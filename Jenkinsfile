
pipeline {
    agent { docker { image 'gcc' } }
    stages {
        stage('Build') {
            steps {
                sh 'gcc -v'
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'gcc Reverse_String_I.c'
                sh './a.out'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Pop me an meesage'
            }
        }
    }
}
