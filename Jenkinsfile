pipeline{
	agent any
	stages{
		stage("Login to docker internal registry"){
			steps{
				sh "docker login registry.planck.ai"
			}
		}
		stage("Pull Latest Image"){
			steps{
				sh "docker pull registry.planck.ai/selenium-docker"
			}
		}
		stage("Start Grid"){
			steps{
				sh "docker-compose up -d hub chrome firefox"
			}
		}
		stage("Run Test"){
			steps{
				sh "docker-compose up search-module book-flight-module"
			}
		}
	}
	post{
		always{
			archiveArtifacts artifacts: 'output/**'
			sh "docker-compose down"
			sh "sudo rm -rf output/"
		}
	}
}
