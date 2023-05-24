pipeline {
	agent any;
	// agent { label node03 }

//	tools{
//        maven "M2"
//	}

 	stages{
			stage('checkout'){
						steps{
								echo "checking out from GitHub"
								git 'https://github.com/devopss1/may23.git'
								
						}
			}

			stage('Build'){
						steps{
								echo "Using maven for build"
								sh 'mvn -f pom.xml clean package'
						}
			}

			stage('Artifactory'){
						steps{
								echo "Upload the artifact to NEXUS"
								nexusArtifactUploader artifacts: [[artifactId: 'myapp', classifier: '', file: 'target/myapp.war', type: 'war']], credentialsId: 'nexus', groupId: 'myapp', nexusUrl: '192.168.0.12:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'snapshots', version: '1.0-SNAPSHOT'
						}
			}

			stage('Deploy'){
						steps{
								echo "Deploy to production"
						}
			}
	}

	post {

		success {
					echo "build is successful"	
				}
		failure{
				echo "Build failed please verify"
		}
	}

}
