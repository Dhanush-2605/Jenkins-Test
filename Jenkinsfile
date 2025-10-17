pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout from your GitHub repo and master branch
                git branch: 'master', url: 'https://github.com/Dhanush-2605/Jenkins-Test.git'
            }
        }

        stage('Set up Python') {
            steps {
                sh '''
                    python3 --version
                    pip3 --version
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    if (fileExists('requirements.txt')) {
                        sh 'pip3 install -r requirements.txt'
                    } else {
                        echo "No requirements.txt found, skipping install."
                    }
                }
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    pip3 install pytest
                    pytest test/ --maxfail=1 --disable-warnings -v
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
        success {
            echo '✅ All tests passed successfully!'
        }
        failure {
            echo '❌ Tests failed. Check logs for details.'
        }
    }
}
