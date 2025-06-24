pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    // Using a more complete Node.js image instead of alpine
                    image 'node:18'
                    reuseNode true
                }
            }
            steps {
                sh '''
                    ls -la
                    node --version
                    npm --version
                    
                    # Install dependencies globally to avoid npm issues
                    npm install -g react-scripts
                    
                    # Install project dependencies
                    npm install --legacy-peer-deps
                    
                    # Build with explicit path to react-scripts
                    export PATH="$PWD/node_modules/.bin:$PATH"
                    echo "PATH: $PATH"
                    which react-scripts || echo "react-scripts not found in path"
                    
                    # Run build with explicit call to react-scripts
                    ./node_modules/.bin/react-scripts build || node_modules/.bin/react-scripts build
                    
                    ls -la
                '''
            }
        }
    }
    post {
        always {
            echo 'Pipeline completed.'
        }
    }
}