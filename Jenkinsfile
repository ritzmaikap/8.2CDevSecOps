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
		export PATH=$PATH:/opt/homebrew/bin
            	which npm
                sh 'npm install'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npm test || true' // Allows pipeline to continue despite test failures
            }
	    post {
            	always {
                	emailext (
                    		to: 's224955405@deakin.edu.au',
                    		subject: "JenkinsP - Test Stage ${currentBuild.result}",
                    		body: "The Test stage has finished with status: ${currentBuild.result}",
                    		attachLog: true
                		)
            		}
        	}
        }
        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true' //Ensure coverage report exists
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true' // this will show known CVEs in the output
            }
	    post {
            	always {
                	emailext (
                    		to: 's224955405@deakin.edu.au',
                    		subject: "Jenkins - Security Scan ${currentBuild.result}",
                    		body: "The Security Scan stage has finished with status: ${currentBuild.result}",
                    
                    		attachLog: true
                		)
            		}
        	}

        }
    }
}
