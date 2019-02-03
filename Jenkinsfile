pipeline {
	parameters {
		string(defaultValue: 'master', description: 'branch to build', name: 'branch', trim: true)
	}
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
		
		stage('test') {
			steps {
				sh 'mvn test'
			}
			post {
				always {
					junit '**/surefire-reports/**/*.xml'
				}
			}
		}
    }
}