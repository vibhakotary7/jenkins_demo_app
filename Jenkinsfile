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
                    // Explicitly load RVM and use the correct Ruby version
                    sh '''
                        source /usr/local/rvm/scripts/rvm || source ~/.rvm/scripts/rvm
                        rvm use 2.6.10 --default
                        gem install bundler -v 2.4.22
                        bundle install
                    '''
                }
            }
        }

        stage('Run Tests') {
            steps {
                script {
                    sh '''
                        source /usr/local/rvm/scripts/rvm || source ~/.rvm/scripts/rvm
                        rvm use 2.6.10
                        bundle exec rake test
                    '''
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    sh '''
                        source /usr/local/rvm/scripts/rvm || source ~/.rvm/scripts/rvm
                        rvm use 2.6.10
                        bundle exec rake build
                    '''
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh '''
                        source /usr/local/rvm/scripts/rvm || source ~/.rvm/scripts/rvm
                        rvm use 2.6.10
                        bundle exec rake deploy
                    '''
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
