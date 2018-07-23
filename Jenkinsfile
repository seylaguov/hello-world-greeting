node ('master') {
    withEnv(['JAVA_HOME=/devops_tools/java/jdk', 'JRE_HOME=/devops_tools/java/jre']) {
		    
	stage('Poll') {
		scm checkout
	}
	
	stage('Build & Unit test') {
		sh 'mvn clean verify -DskipITs=true';
		junit '**/target/surefire-reports/TEST-*.xml'
		archive 'target/*.jar'
	}
	
	stage('Static Code Analysis') {
		sh 'mvn clean verify sonar:sonar -Dsonar.projectName=example-project -Dsonar.projectKey=example-project -Dsonar.projectVersion=$BUILD_NUMBER';
	}
	
	stage ('Integration Test'){
		sh 'mvn clean verify -Dsurefire.skip=true';
		junit '**/target/failsafe-reports/TEST-*.xml'
		archive 'target/*.jar'
	}
    }
}
