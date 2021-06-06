pipeline{
agent any
tools {maven 'localMaven'
	jdk 'localJdk'
}
stages{
	stage('Build'){
		steps{
			sh 'mvn clean package'
		}
	post{
		success{
			echo ' now Archiving '
			archiveArtifacts artifacts: '**/*.war'
		}
		}
	}
	stage('SonarQube Scan'){
		steps{
			sh """mvn sonar:sonar \
			      -Dsonar.host.url=http://54.191.253.170:9000 \
			      -Dsonar.login=5729e6994dbbae5dfe326a7214b85fabae15a0e8"""
		}
	}
	stage('Deploy to Staging'){
			steps{
				sh "mvn clean deploy -s /home/ec2-user/.m2/settings.xml -DskipTests"
			}
			
		}

}

}
