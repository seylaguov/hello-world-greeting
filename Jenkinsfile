node ('master') {
    
    withEnv(['JAVA_HOME=/devops_tools/java/jdk', 'JRE_HOME=/devops_tools/java/jre']) {
	checkout scm	
	
	stage('Build') {
		 withMaven(maven: 'M3') {
			sh 'mvn clean verify -DskipITs=true'
		 }
	}
	    
	stage('SonarQube analysis') {
		withSonarQubeEnv('SQ Server') {
			// requires SonarQube Scanner for Maven 3.2+
			sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
		}
	}
	    
        stage('Results') {
            junit '**/target/surefire-reports/TEST-*.xml'
            archive 'target/*.jar'
	}

    }
}
