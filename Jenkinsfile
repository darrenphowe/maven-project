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
}
}