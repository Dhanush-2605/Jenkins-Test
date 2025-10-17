pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo '📦 Cloning repository...'
                git branch: 'main', url: 'https://github.com/<your-username>/<your-repo>.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo '📥 Installing dependencies...'
                sh '''
                    python3 -m venv venv
                    source venv/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                echo '🧪 Running Pytest...'
                sh '''
                    source venv/bin/activate
                    pytest --html=report.html --self-contained-html
                '''
            }
        }
    }

    post {
        success {
            echo '✅ All tests passed successfully!'
        }
        failure {
            echo '❌ Some tests failed. Check Jenkins logs or the report.html file.'
        }
    }
}
