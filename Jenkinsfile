pipeline{
agent any
stages{
tools {maven 'localMaven'}
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
