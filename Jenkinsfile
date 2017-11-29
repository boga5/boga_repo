
node{

//Build Stage and SonarQube 

	stage ('Build') {
			checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory']], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/SnehaKailasa/boga_repo.git']]])
	sh '''./testing.sh'''
	
	}
}

