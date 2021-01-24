node(){

		def repoURL='https://github.com/muhammadfarhansoomro/TestNGCucumberLearning.git'

		stage("Prepare Workspace"){
			cleanWs()
			env.WORKSPACE_LOCAL=sh(returnStdout:true,script:'pwd').trim()
			echo"Workspace set to:"+env.WORKSPACE_LOCAL
		}
		stage('Checkout Self'){
		git branch:'main',credentialsId:'',url:repoURL
		}
		tools { 
		maven 'Maven 3.5.4'
	   	 }
		stage('Cucumber Tests'){
			withMaven(maven:'/usr/maven/bin'){
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
