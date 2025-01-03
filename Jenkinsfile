pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from the Git repository
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                script {
                    // Install Python 3 and dependencies if not installed
                    sh '''
                        if ! command -v python3 &> /dev/null; then
                            echo "Python3 not found, installing..."
                            apt-get update && apt-get install -y python3 python3-pip python3-venv python3-flask
                        fi
                    '''
                }
                echo 'Creating virtual environment and installing dependencies...'
                sh '''
                    python3 -m venv venv
                    source venv/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh '''
                    source venv/bin/activate
                    python3 -m unittest discover -s .
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                // Add deployment steps here
            }
        }

        stage('Run Application') {
            steps {
                echo 'Running application...'
                // Add steps to run the application here
            }
        }
        
        stage('Test Application') {
            steps {
                echo 'Testing application...'
                // Add application testing steps here
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh 'deactivate'
        }
    }
}
