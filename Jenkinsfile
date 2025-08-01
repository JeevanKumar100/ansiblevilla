pipeline {
    agent any

    environment {
        // Optional: Set any environment variables here
        DEPLOY_ENV = "production"
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo "Cloning application repository..."
                git branch: 'main', url: 'https://github.com/JeevanKumar100/ansiblevilla.git'
            }
        }

        stage('Install Dependencies on Jenkins') {
            steps {
                echo "Ensuring Ansible is installed..."
                sh '''
                    if ! command -v ansible >/dev/null 2>&1; then
                        sudo apt update && sudo apt install -y ansible
                    fi
                '''
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                echo "Running Ansible playbook for deployment..."
                sh '''
                    ansible-playbook deploy.yml
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Deployment completed successfully.'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}

