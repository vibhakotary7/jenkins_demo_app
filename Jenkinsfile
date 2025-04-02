pipeline {
    agent any

    stages {
        stage('Verify rbenv Installation') {
            steps {
                script {
                    sh '''
                        echo "Checking rbenv installation..."
                        which rbenv || echo "rbenv not found"
                        rbenv root || echo "rbenv root not found"
                    '''
                }
            }
        }

        stage('Verify Ruby Version') {
            steps {
                script {
                    sh '''
                        echo "Verifying Ruby version managed by rbenv..."
                        export PATH="$HOME/.rbenv/bin:$PATH"
                        eval "$(rbenv init -)"
                        rbenv global 3.1.0

                        echo "Ruby version:"
                        ruby -v

                        echo "List of installed Ruby versions:"
                        rbenv versions

                        echo "Active Ruby version path:"
                        rbenv which ruby
                    '''
                }
            }
        }

        stage('Verify Environment Variables') {
            steps {
                script {
                    sh '''
                        echo "Environment Variables:"
                        env | grep -E 'RBENV|PATH'
                    '''
                }
            }
        }
    }

    post {
        always {
            echo 'Verification completed.'
            cleanWs()
        }
        success {
            echo 'rbenv and Ruby version successfully configured!'
        }
        failure {
            echo 'rbenv or Ruby configuration failed. Check the logs.'
        }
    }
}
