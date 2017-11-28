//General settings will be in UI

node{

//Build Stage and SonarQube 

	stage ('Build') {
//Multiple SCMs trial by boga **************
		// first repository
		checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory']], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/boga5/java-app.git']]])
		// second repository
		//checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'lmsqa']], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'c0c5e22f-9121-4734-922d-d8bfb1c4e339', url: 'https://padlgithubggk1.sw.fortna.net/GGK-sboga/ggk-wes-service-lms-qa.git']]])
//trial code ends here ************
		sh '''service=wes-service-lms-0.0.1-${BUILD_NUMBER}.jar 
		//sed -i "s/jarfile/$service/" src/main/docker/Dockerfile'''
		withSonarQubeEnv {
		// some block
			def mvn_version = tool 'maven'
			echo "${mvn_version}"
			withEnv( ["PATH+MAVEN=${mvn_version}/bin"] ) {
				sh "mvn clean package docker:build -Dbuild.number=${BUILD_NUMBER} $SONAR_MAVEN_GOAL -Dsonar.host.url=$SONAR_HOST_URL -Dsonar.projectKey=jenkins-file -Dsonar.projectName=jenkins-file"
				}
		}    
	}

	//Docker Image
	stage ('dockerpush') {
		sh '''docker image tag fortna/wes-service-lms-0.0.1-${BUILD_NUMBER} 10.240.17.12:5043/wes-service-lms-1.0.0_jenkinsfile'''
		docker.withRegistry("https://10.240.17.12:5043", '4c82b77f-680b-4e99-8b1f-30a263f98e21'){
		def customImage = docker.image('10.240.17.12:5043/wes-service-lms-1.0.0_jenkinsfile')
		customImage.push()
		}
	}

	//Hosting Docker container
	stage ('deployment') {      
		sh '''#!/bin/bash
		Container_status=`docker ps -a | grep "fortna-lms_jenkinsfile"`
		if [ ! -z "$Container_status" ];
		then
			docker rm fortna-lms_jenkinsfile -f
		fi
		docker run -it -d --name fortna-lms_jenkinsfile --privileged=true -p 3000:8082 --add-host=dbserver:192.168.13.14 --env SERVICE_NAME=lms --env SERVICE_ID=lms_cicd -v /tmp/logs/lms/logs:/logs -v /tmp/logs/lms/configs:/configs 10.240.17.12:5043/wes-service-lms-1.0.0_jenkinsfile'''
	}
   
/* Certificate Issue for Deploying Artifacts
	stage ('Deploy Artifacts') {
	def server = Artifactory.newServer url: 'https://padlcicdggk4.sw.fortna.net/artifactory/webapp/', credentialsId: '067a8aaf-47b1-4cb4-99a0-44bcfd01bbc9'
	def buildInfo = Artifactory.newBuildInfo()
	buildInfo.env.capture = true
	def rtMaven = Artifactory.newMavenBuild()
	//rtMaven.tool = MAVEN_TOOL // Tool name from Jenkins configuration
	//rtMaven.opts = "-Denv=dev"
	rtMaven.deployer releaseRepo:'develop-release', snapshotRepo:'develop-snapshot', server: server
	rtMaven.resolver releaseRepo:'develop-release', snapshotRepo:'develop-snapshot', server: server
	//rtMaven.run pom: 'pom.xml', goals: 'clean install', buildInfo: buildInfo
	buildInfo.retention maxBuilds: 10, maxDays: 7, deleteBuildArtifacts: true
	//Publish build info.
	server.publishBuildInfo buildInfo
	}
    
code ends here */    
    
	stage ('RFW') {
	sh '''sleep 20s 
	pybot --variable hostname:10.240.17.11 --variable port:6051 lmsqa/tests/sampletest.robot'''
	step([$class: 'RobotPublisher',
	outputPath: '.',
	passThreshold: 50,
	unstableThreshold: 50,
	otherFiles: ""])
	}
}
