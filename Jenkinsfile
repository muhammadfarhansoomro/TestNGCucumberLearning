node(){
		def repoURL='https://github.com/muhammadfarhansoomro/TestNGCucumberLearning.git'

		stage("Prepare Workspace"){
			cleanWs()
			env.WORKSPACE_LOCAL=sh(returnStdout:true,script:'pwd').trim()
			echo"Workspace set to:"+env.WORKSPACE_LOCAL
		}
	stage('JIRA') {
   		 def serverInfo = jiraGetServerInfo site: '192.168.253.1:8090', failOnError: false
		echo serverInfo.data.toString()
    		}
		stage('Checkout Self'){
		git branch:'main',credentialsId:'',url:repoURL
		}
		stage('Cucumber Tests'){
			withMaven(maven:'Maven35'){
				sh """
					cd ${env.WORKSPACE_LOCAL}
					mvn clean test
				"""
			}
		}
		stage('Expose report'){
			archive "**/cucumber.json"
			cucumber '**/cucumber.json'
		}
  }
