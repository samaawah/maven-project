pipeline{
agent any
tools {maven 'localMaven'
	java 'localJdk'
}
stages{
	stage('Build'){
		steps{
			powershell 'mvn clean package'
		}
	post{
		success{
			echo ' now Archiving '
			archiveArtifacts artifacts: '**/*.war'
		}
		}
	}
}

}
