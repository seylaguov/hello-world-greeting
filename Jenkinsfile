node ('master') {
    
    withEnv(['JAVA_HOME=/devops_tools/java/jdk', 'JRE_HOME=/devops_tools/java/jre']) {
	checkout scm	
	
	stage('Build') {
		 withMaven(maven: 'M3') {
			sh 'mvn clean verify -DskipITs=true'
		 }
	}
    
        stage('Results') {
            junit '**/target/surefire-reports/TEST-*.xml'
            archive 'target/*.jar'
	}
	    
	stage('Static Code Analysis') {
		sh 'mvn clean verify sonar:sonar -Dsonar.projectName=example-project -Dsonar.projectKey=example-project -Dsonar.projectVersion=$BUILD_NUMBER';
	}
    }
}
