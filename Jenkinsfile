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
                    // Set the correct Ruby version using rbenv or RVM
                    sh '''
                        export PATH="$HOME/.rbenv/bin:$PATH"
                        if command -v rbenv >/dev/null; then
                            eval "$(rbenv init -)"
                        fi
                        ruby -v
                        gem update --system
                        gem install bundler
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
