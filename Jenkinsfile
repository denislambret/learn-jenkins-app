pipeline {
    agent any

    environment {
        BUILD_FILE_NAME = 'Laptop.txt'    
    }
    
    stages {
        stage('Initialisation') {
            steps {
                cleanWs()
                sh ''' 
                    touch ./init.conf
                    echo "hello local">>./init.conf
                '''
            }
        }
    
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode false
                }
            }
            steps {
                echo 'Check current npm version ...'
                sh 'npm --version'
                
                echo 'Create remote file...'
                sh ''' 
                    touch ./init.conf
                    echo "hello remote">>./init.conf
                '''
                
            }
        }
    }
    
    post {
        success {
           echo 'npm node created'
        }
        unsuccessful {
           echo 'npm node not created'
        }
        
    }
}
