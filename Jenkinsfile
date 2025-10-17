


pipeline {
    agent any

    environment {
        PYTHON = '/usr/bin/python3'
    }

    stages {

        stage('Checkout Code') {
            steps {
                echo "📦 Checking out code from GitHub..."
                git branch: 'master', url: 'https://github.com/Dhanush-2605/Jenkins-Test.git'
            }
        }

        stage('Setup Environment') {
            steps {
                echo "⚙️ Setting up virtual environment..."
                sh '''
                    sudo apt update
                    sudo apt install -y python3-venv python3-pip
                    ${PYTHON} -m venv venv
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "📥 Installing dependencies..."
                sh '''
                    . venv/bin/activate
                    python -m pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                echo "🧪 Running tests using pytest..."
                sh '''
                    . venv/bin/activate
                    pytest --maxfail=1 --disable-warnings -q --html=report.html
                '''
            }
        }

        stage('Archive Test Report') {
            steps {
                echo "📊 Archiving pytest report..."
                archiveArtifacts artifacts: 'report.html', fingerprint: true
            }
        }
    }

    post {
        success {
            echo "✅ Build & tests successful!"
        }
        failure {
            echo "❌ Some tests failed. Check report.html in Jenkins artifacts."
        }
    }
}
