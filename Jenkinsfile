pipeline {
    agent {
        node {
            label 'master'
        }
    }
    stages { 	
        stage('Build Jar') {
            steps {
                sh 'package -DskipTests'
            }
        }
        stage('Build Image') {
            steps {
                script {
                	app = docker.build("gkarnati/containertest")
                }
            }
        }
        stage('Push Image') {
            steps {
                script {
			        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
			        	app.push("${BUILD_NUMBER}")
			            app.push("latest")
			        }
                }
            }
        }        
    }
}