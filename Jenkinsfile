// Powered by Infostretch 

timestamps {

node () {

	stage ('Tyler Test - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git-login', url: 'https://github.com/bendavidtyler/jenkins-sample']]]) 
	}
	stage ('Tyler Test - Build') {
 			// Maven build step
	withMaven(maven: 'Maven') { 
 			if(isUnix()) {
 				sh "mvn clean " 
			} else { 
 				bat "mvn clean " 
			} 
 		}		// Maven build step
	withMaven(maven: 'Maven') { 
 			if(isUnix()) {
 				sh "mvn compile " 
			} else { 
 				bat "mvn compile " 
			} 
 		}		// Maven build step
	withMaven(maven: 'Maven') { 
 			if(isUnix()) {
 				sh "mvn test " 
			} else { 
 				bat "mvn test " 
			} 
 		}		// Maven build step
	withMaven(maven: 'Maven') { 
 			if(isUnix()) {
 				sh "mvn package -DskipTests " 
			} else { 
 				bat "mvn package -DskipTests " 
			} 
 		} 
	}
	stage('Quality check') {
		withSonarQubeEnv('Sonar') {
		bat "mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=Tyler_Test1"
		}
	} 
	
	stage ('Tyler Test - Post build actions') {
/*
Please note this is a direct conversion of post-build actions. 
It may not necessarily work/behave in the same way as post-build actions work.
A logic review is suggested.
*/
		// Mailer notification
		step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: 'ben.tyler@st.com', sendToIndividuals: false])
 
	}
}
}
