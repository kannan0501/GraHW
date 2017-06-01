node { 
	checkout scm
	env.PATH ="${tool 'gradle'}/bin:${env.PATH}"
	stash excludes: 'target/', includes: '**', name: 'source'
	emailext attachLog: true,body: 'Test', compressLog: true, subject: 'Test jenkins Pipelines', to: 'sgandra@altimetrik.com,snachiappan@altimetrik.com' 
	properties([pipelineTriggers([cron('0 10 * * *')])])
	stage('validate') {
		sh 'gradle validate'
	} 
	stage('compile') {
		sh 'gradle compile'
	} 
	stage('package') {
		 sh 'gradle clean package -DskipTests'
	}
	stage('install') {
		sh 'gradle clean install'
	} 
	stage('test') {
		parallel 'integration': {
			sh 'gradle clean verify'
		}, 'quality': {
			//sh 'mvn sonar:sonar'
			} 
	} 
	/*stage('deploy') {
		unstash 'source'
		sh 'cp target/*.jar /opt/deploy'
	}*/
}
