node {
	def temp1 = null
	stage ('Checkout SCM') {
		checkout scm//([$class: 'GitSCM', branches: [[name: '*/branch1']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/boga5/boga_repo.git']]])	
		//checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', name: '', refspec: '', url: 'https://github.com/boga5/boga_repo.git']]]
	}
	
	stage ('Test Build') {
		sh """ echo ${JOB_NAME}
		temp=${JOB_NAME}
		"""
		sh """ echo hi ${temp} """
		
	}
		
		stage ('Reading Branch Varibles ')	{
			println temp
			Reason = "lockVar stage Failed"
			JobName = "${JOB_NAME}"
			def branch_name1 = properties.branch_name
			println "${branch_name1}" 
			if(JobName.contains('PR-'))
			{
				def index = JobName.indexOf("/");
				lockVar = JobName.substring(0 , index)+"_"+"${branch_name1}"
				Sonar_project_name = lockVar + "PR" 
			}
			else
			{
				 def index = JobName.indexOf("/");
				 Sonar_project_name = JobName.substring(0 , index)+"_"+"${BRANCH_NAME}"
				 lockVar = Sonar_project_name
			}
		
	
		
	}
}
