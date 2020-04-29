pipeline {
    agent any
    stages {
        stage('Lint HTML') {
            steps {
                sh 'echo Linting HTML'
                sh 'tidy -q -e *.html'
            }
        }
        stage('Upload to AWS') {
            steps {
                retry(3) {
                    withAWS(region:'us-west-2', credentials: 'aws-static') {
                        s3Upload(file:'index.html', bucket:'udacity-project3-jenkins', path:'index.html')
                    }
                }
            }
        }
        stage('Health check') {
            steps {
                sh 'curl --silent --fail "http://udacity-project3-jenkins.s3-website.us-west-2.amazonaws.com" >/dev/null'
            }
        }
    }
}