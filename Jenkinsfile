pipeline {
    agent any
    tools {
        maven 'maven'
    }

    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
        stage ('Build') {
            steps {
                sh 'mvn clean package'
            }
            post {
                    success {
                        junit 'target/surefire-reports/**/*.xml'
                 }
            }
        }
         
	    stage('SonarQuebeServer') {
    environment {
        scannerHome = tool 'SonarQuebeScanner'
    }
    steps {
        withSonarQubeEnv('SonarQuebeServer') {
            sh "${scannerHome}/bin/sonar-scanner"
        }
        timeout(time: 10, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: true
        }
    }
}
        
    }
    
 
  }

