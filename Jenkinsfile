pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''
                    mkdir -p build
                    cp assingment.html build/index.html
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    test -s build/index.html
                    grep -qi '<html' build/index.html
                    echo "HTML checks passed"
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    install -m 644 build/index.html /var/www/html/devops-lab/index.html
                    curl --fail --silent --show-error http://localhost/devops-lab/ -o deployed-check.html
                    cmp build/index.html deployed-check.html
                    echo "Deployment verified successfully"
                '''
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'build/index.html'
        }
    }
}