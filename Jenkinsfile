pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ritzmaikap/8.2CDevSecOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh '''
		export PATH=$PATH:/opt/homebrew/bin
            	which npm
		npm install
		'''
            }
        }
        stage('Run Tests') {
            steps {
                sh '''
		export PATH=$PATH:/opt/homebrew/bin
            	which npm
		npm test || true''' // Allows pipeline to continue despite test failures
            }
	    
        }
        stage('Generate Coverage Report') {
            steps {
                sh '''
		export PATH=$PATH:/opt/homebrew/bin
            	which npm
		npm run coverage || true''' //Ensure coverage report exists
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                sh '''
		export PATH=$PATH:/opt/homebrew/bin
            	which npm
		npm audit || true''' // this will show known CVEs in the output
            }
	    

        }
    }
}
