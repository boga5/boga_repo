node {
	stage ('Checkout SCM') {
		checkout scm//([$class: 'GitSCM', branches: [[name: '*/branch1']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/boga5/boga_repo.git']]])	
		//checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', name: '', refspec: '', url: 'https://github.com/boga5/boga_repo.git']]]
	}
	
	stage ('Test Build') {
		println env.JOB_NAME
		println env.BRANCH_NAME
	}
}
