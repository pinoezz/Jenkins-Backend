def secret = 'pinoezz'
def server = 'jenkins@103.171.85.155'
def dir = 'wayshub-backend'
def branch = 'master'

pipeline{
	agent any
	stages{
		stage ('Delete container and images & git pull'){
			steps{
				sshagent([secret]) {
					sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
					cd ${dir}
					docker-compose down
					docker system prune -f
					git pull origin ${branch}
					exit
					EOF"""
				}
			}
		}
	stage ('Build Images'){
                        steps{
                                sshagent([secret]) {
                                        sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                                        cd ${dir}
                                        docker-compose build
                                        exit
                                        EOF"""
                                }
                        }
                }
	stage ('Deploy Container'){
                        steps{
                                sshagent([secret]) {
                                        sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
                                        cd ${dir}
                                        docker-compose up -d
                                        exit
                                        EOF"""
                                }
				
                        }
		
               }

	}
	
}
