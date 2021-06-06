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
	}
	stage('Deploy to Staging'){
			steps{
				build job: 'deploy-to-staging'
			}
			
		}
	stage ('Deploy to Production'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }

                build job: 'deploy-to-production'
            }
            post {
                success {
                    echo 'Code deployed to Production.'
                }

                failure {
                    echo ' Deployment failed.'
                }
            }
        }
}

}
