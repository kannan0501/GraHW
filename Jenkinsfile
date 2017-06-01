node { 
	checkout scm
	checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/kannan0501/GraHW.git']]]) 
	//env.PATH ="${tool 'gradle'}/bin:${env.PATH}"
	stash excludes: 'target/', includes: '**', name: 'source'
	//emailext attachLog: true,body: 'Test', compressLog: true, subject: 'Test jenkins Pipelines', to: 'sgandra@altimetrik.com,snachiappan@altimetrik.com' 
	//properties([pipelineTriggers([cron('0 10 * * *')])])
	stage('clean') {
		sh 'gradle clean'
	} 
	stage('build') {
		sh 'gradle build'
	} 
	stage('test') {
		 sh 'gradle test'
	}
	/*stage('install') {
		sh 'gradle clean install'
	} 
	stage('test') {
		parallel 'integration': {
			sh 'gradle clean verify'
		}, 'quality': {
			//sh 'mvn sonar:sonar'
			} 
	} 
	stage('deploy') {
		unstash 'source'
		sh 'cp target/*.jar /opt/deploy'
	}*/
}
