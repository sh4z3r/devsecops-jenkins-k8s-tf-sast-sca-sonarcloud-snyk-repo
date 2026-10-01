pipeline {
  agent any
  tools { 
        maven 'Maven_3.5.2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
				withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
					sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=dsi-test -Dsonar.organization=dsi-test -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=${SONAR_TOKEN}'
				}
			}
    }

	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }		
  }
}
