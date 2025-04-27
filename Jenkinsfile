pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=infectedwebapp -Dsonar.organization=infectedwebapp -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=6535f35559dcc0ab8ef38234b138063be3a652da'
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
