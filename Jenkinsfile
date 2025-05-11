pipeline {
    agent any

    environment {
        DEPLOY_DIR = "/var/www/html"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', credentialsId: 'your-credentials-id', url: 'https://github.com/Nivethitha-24/project.git'
            }
        }

        stage('Deploy to Server') {
            steps {
                sh '''
                echo "Starting Deployment..."

                # Ensure Jenkins has permission to modify /var/www/html
                sudo chown -R jenkins:jenkins $DEPLOY_DIR
                sudo chmod -R 755 $DEPLOY_DIR

                # Remove old files
                sudo rm -rf $DEPLOY_DIR/*

                # Copy new files
                sudo cp -r * $DEPLOY_DIR/

                # Restart Apache server
                sudo systemctl restart apache2

                echo "Deployment successful!"
                '''
            }
        }
    }
}
