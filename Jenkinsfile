node {
	stage ('Checkout SCM') {
		checkout([$class: 'GitSCM', branches: [[name: '*/branch1']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/boga5/boga_repo.git']]])	
		//checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', name: '', refspec: '', url: 'https://github.com/boga5/boga_repo.git']]]
	}
	
	stage ('Test Build') {
		sh '''ls -la file.sh'''
		sh '''chmod 774 file.sh'''
		sh '''./file.sh'''
	}
}
