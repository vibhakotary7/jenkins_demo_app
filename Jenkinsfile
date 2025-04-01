pipeline {
    agent any

    environment {
        RAILS_ENV = 'test'
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/yourusername/jenkins_demo_app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'gem install bundler'
                sh 'bundle install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'rails test'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the Rails application...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
            }
        }
    }
}
