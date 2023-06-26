pipeline {
  agent any
  tools { 
    maven 'Maven_3_5_2'  
  }
  stages{
    stage('CompileandRunSonarAnalysis') {
      steps {	
		    sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=apm -Dsonar.organization=nmhieuit -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=05aad7e881d3f4e7d0a45fa672f4b1bea90bd70f'
			}
    }
  }
}
