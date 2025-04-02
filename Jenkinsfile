pipeline {
    agent any
    environment {
        // Correctly concatenate the PATH with additional directories
        PATH = "/Users/vibha/.rbenv/bin:/Users/vibha/.rbenv/shims:${env.PATH}"
    }

    stages {
        stage('Verify rbenv Installation') {
            steps {
                script {
                    sh '''
                        echo "Step 1: Checking rbenv installation..."
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
                        echo "Step 2: Verifying Ruby version managed by rbenv..."
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
                        echo "Step 3: Printing Environment Variables..."
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
