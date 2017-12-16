node {
	def temp1 = null
	stage ('Checkout SCM') {
		checkout scm
	}
	
	def content = readFile './.env'				// variable to store .env file contents
	Properties properties = new Properties()	// creating an object for Properties class
	InputStream contents = new ByteArrayInputStream(content.getBytes());	// storing the contents
	properties.load(contents)	
	contents = null
	def branch_name1 = properties.branch_name
	def res
	stage ('Reading Branch Varibles ')	{
		println env.JOB_NAME
		println branch_name1
		sh """ res=`echo ${env.JOB_NAME}``echo _` 
		echo \${res} """
		println res+"hello"
	}
}
