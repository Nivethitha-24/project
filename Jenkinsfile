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
                echo "jenkins-password" | sudo -S chown -R jenkins:jenkins $DEPLOY_DIR
                echo "jenkins-password" | sudo -S chmod -R 755 $DEPLOY_DIR

                # Remove old files
                echo "jenkins-password" | sudo -S rm -rf $DEPLOY_DIR/*

                # Copy new files
                echo "jenkins-password" | sudo -S cp -r * $DEPLOY_DIR/

                # Restart Apache server
                echo "jenkins-password" | sudo -S systemctl restart apache2

                echo "Deployment successful!"
                '''
            }
        }
    }
}
