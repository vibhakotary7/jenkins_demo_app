pipeline {
    agent any

    stages {
        stage('Verify rbenv Installation') {
            steps {
                script {
                    sh '''
                        echo "Step 1: Loading custom environment for Jenkins..."
                        source ~/jenkins_env.sh

                        echo "Step 2: Checking rbenv installation..."
                        which rbenv || echo "rbenv not found"
                        rbenv root || echo "rbenv root not found"

                        echo "Step 3: Rehashing rbenv..."
                        rbenv rehash || echo "rbenv rehash failed"
                    '''
                }
            }
        }

        stage('Verify Ruby Version') {
            steps {
                script {
                    sh '''
                        echo "Step 4: Verifying Ruby version managed by rbenv..."
                        source ~/jenkins_env.sh
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
                        echo "Step 5: Printing Environment Variables..."
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
