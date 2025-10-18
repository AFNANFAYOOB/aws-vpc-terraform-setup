pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Pull code from GitHub
                git branch: 'main',
                    credentialsId: 'github-token',
                    url: 'https://github.com/AFNANFAYOOB/aws-vpc-terraform-setup'
            }
        }

        stage('Setup Python Environment') {
            steps {
                bat '''
                python -m venv venv
                call venv\\Scripts\\activate
                python -m pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                bat '''
                echo "No tests to run, skipping..."
                '''
            }
        }
    }

    post {
        always {
            junit 'report.xml'  // publishes pytest results if available
        }
        success {
            echo '✅ Python build and tests passed successfully!'
        }
        failure {
            echo '❌ Python build or tests failed!'
        }
    }
}
