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
	stage{
		withSonarQubeEnv('SonarCloud') {
    		sh "sonar:sonar -Dsonar.branch.name=${env.BRANCH_NAME}"
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
