pipeline {
    agent any

    stages {
	
	 stage('clean dir before start') {
            steps {
				dir('')
                     {
						deleteDir()
            }
        }
    }
	
	 stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: '8087fba5-176a-4569-982a-02b6380b63a7', url: 'https://github.com/dkdhruvkhandelwal67/TrainingRepo.git']]])
            }
        }
		
        stage('Performance test') {
            steps {
                 dir('training/')
                     {
                bat  "C:\\Users\\Dhruv.Khandelwal\\Desktop\\Training\\JmeterCourse\\apache-jmeter-5.5\\bin\\jmeter.bat -n -t JmeterJenkinsTest.jmx -l test.jtl"
				}
			}
		}
		
		stage('Generate Performance test Stats') {
            steps {
                 dir('training/')
                     {
					perfReport errorFailedThreshold: 0, errorUnstableThreshold: 0, filterRegex: '', ignoreFailedBuilds: true, ignoreUnstableBuilds: true, junitOutput: 'test.jtl', modeEvaluation: true, persistConstraintLog: true, sourceDataFiles: 'test.jtl'
				}
			}
		}
	}
}
