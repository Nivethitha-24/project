pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'git@github.com:yourusername/your-static-site.git'
            }
        }

        stage('Deploy') {
            steps {
                // If deploying to local Jenkins workspace (for testing)
                // Just archive the files, or copy to web server folder
                
                // If deploying to remote server via SSH:
                sshagent(['your-ssh-credential-id']) {
                    sh '''
                       rsync -avz --delete ./ user@yourserver:/var/www/html/
                    '''
                }
            }
        }
    }
}
