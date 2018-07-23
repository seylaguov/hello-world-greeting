node ('master') {
    
    withEnv(['JAVA_HOME=/devops_tools/java/jdk', 'JRE_HOME=/devops_tools/java/jre']) {
	checkout scm
	    
        withMaven(maven: 'M3') {
	
		stage('Build & Unit test') {
			sh 'mvn clean verify -DskipITs=true';
			junit '**/target/surefire-reports/TEST-*.xml'
			archive 'target/*.jar'
		}

		stage('Results') {
		    junit '**/target/surefire-reports/TEST-*.xml'
		    archive 'target/*.jar'
		}

		stage('SonarQube analysis') {
			//def sonarqubeScannerHome = tool name: 'default', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
			withSonarQubeEnv('default') {
				// requires SonarQube Scanner for Maven 3.2+
				//sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
				sh 'mvn clean verify sonar:sonar -Dsonar.projectName=example-project -Dsonar.projectKey=example-project -Dsonar.projectVersion=$BUILD_NUMBER';
				//sh "${sonarqubeScannerHome}/bin/sonar-runner -Dsonar.host.url=${SONAR_HOST_URL}  -Dsonar.login=${SONAR_AUTH_TOKEN}    -Dsonar.projectName=xxx -Dsonar.projectVersion=xxx -Dsonar.projectKey=xxx -Dsonar.sources=./src/main"
			}
		}
	}
    }
}

