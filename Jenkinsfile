pipeline {
    agent any
    tools {
        maven 'maven-3.5.0'
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
         
        
    }
    
 
  }


node {
  stage('SCM') {
    git 'https://github.com/PrabalSinghSenger/demo'
  }
  stage('SonarQube analysis') {
    withSonarQubeEnv(
	  credentialsId: 'squ_fd8310db13eac19fefeecc332f8fa455b6f15ebe', 
	  installationName: 'SonarQuebeScanner') { 
	  // You can override the credential to be used
      sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.7.0.1746:sonar'
    }
  }
}
}
}
