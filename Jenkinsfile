pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/vibhakotary7/jenkins_demo_app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Install compatible bundler version
                    sh '''
                        ruby -v
                        gem install bundler -v 2.4.22
                        bundle install
                    '''
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh 'bundle exec rake test'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    sh 'bundle exec rake build'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh 'bundle exec rake deploy'
                }
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs()
        }
        success {
            echo 'Build and Deployment Successful!'
        }
        failure {
            echo 'Build Failed!'
        }
    }
}
