pipeline {
    agent {
        node {
            label 'built-in'
            customWorkspace '/root/Container/'  // Properly placed within the node block
        }
    }
    
    stages {
        stage('Create Container') {
            steps {
                script {
                    // Stop and remove the existing container if it exists, then create a new one
                    sh '''
                    if [ $(docker ps -aq -f name=container) ]; then
                        docker rm -f container
                    fi
                    docker run -dp 80:80 --name container httpd
                    '''
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    // Ensure index.html exists before copying
                    if (fileExists('index.html')) {
                        sh '''
                        docker cp index.html container:/usr/local/apache2/htdocs/
                        docker exec container chmod 755 /usr/local/apache2/htdocs/index.html
                        '''
                    } else {
                        error 'index.html file not found!'
                    }
                }
            }
        }
    }
}
