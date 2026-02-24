pipeline {
	agent any 
	
	stages {

	stage('PULL') {
		steps{
			git 'https://github.com/HarshCraft/CICD-project.git'
		}
	}
	stage('BULD') {
		steps{
		dir('backend') {
			sh'''
			mvn clean package -DskipTests
			'''
			}
		}
	}
	 stage('TEST') {
            steps {
                    dir('backend') {
                            sh '''mvn sonar:sonar \\
                                  -Dsonar.projectKey=sonarp \\
                                  -Dsonar.projectName=\'sonarp\' \\
                                  -Dsonar.host.url=http://13.203.42.107:9000 \\
                                  -Dsonar.token=sqp_e402a316649c94625eb457c8adeb33f28c5025c4
				'''
                    
                }
            }
	stage('QUALITY-GATES') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        }	 

	}
} 
	

