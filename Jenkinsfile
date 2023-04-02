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
	    
	    
	    stage('SonarQube analysis') {
   steps {
      withSonarQubeEnv('SonarQuebeServer') {
         sh 'mvn sonar:sonar -Dsonar.login=sqa_5ea306726a93148ddf4d44d102cadeaa4bf62d7f'
      }
   }
}

        
    }
    
 
  }

