pipeline{
agent any
tools {maven 'localMaven'
	jdk 'localJdk'
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
