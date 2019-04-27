pipeline{
agent any
stages{
	stage('Build'){
		steps{
			psh 'mvn clean package'
		}
	}
	
	post{
		
		success{
			echo ' now Archiving '
			archiveArtifacts artifacts: '**/target/*.war'
		}
	}
}

}