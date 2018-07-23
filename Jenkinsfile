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
    }
}
