timestamps {

node () {

	stage ('package - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/darrenphowe/maven-project.git']]]) 
	}
	stage ('package - Build') {
 			// Maven build step
	withMaven(maven: 'Maven3.6') { 
 			if(isUnix()) {
 				sh "mvn clean package " 
			} else { 
 				bat "mvn clean package " 
			} 
 		}
		archiveArtifacts allowEmptyArchive: false, artifacts: '**/*.war', caseSensitive: true, defaultExcludes: true, fingerprint: true, onlyIfSuccessful: false 
	}
    stage ('deploy - staging') {
    deploy adapters: [tomcat8(credentialsId: 'f98e1c2c-7ca5-433a-889f-271ea935ddc1', path: '', url: 'http://tomcat-docker-staging:8080/')], contextPath: 'webapp', onFailure: false, war: '**/*.war'
   	}
}
}