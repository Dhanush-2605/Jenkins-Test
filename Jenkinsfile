pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo '📦 Cloning repository...'
                git branch: 'master', url: 'https://github.com/Dhanush-2605/Jenkins-Test.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo '📥 Installing dependencies now...'
                sh '''
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                echo '🧪 Running Pytest now...'
                sh '''
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
