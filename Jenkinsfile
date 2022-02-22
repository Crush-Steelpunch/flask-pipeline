pipeline {
    agent any
	environment {
	DATABASE_URI="sqlite:///lr.db"
	SECRET_KEY="password123"
	}
    stages {
        stage('checkout') {
            steps {
		checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Crush-Steelpunch/todo-app-v4.git']]])
            }
        }
        stage('environment and deps and init database') {
		steps{
			withPythonEnv ('python3.6.8'){
				sh "python3 -m pip install -r requirements.txt"
				sh "python3 create.py"
			}
		}
        }
        stage('testing') {
            steps {
			withPythonEnv ('python3.6.8'){
				sh "python3 -m pytest ."
			}
            }
        }
        stage('run app') {
            steps {
			withPythonEnv ('python3.6.8'){
				sh "python3 app.py"
			}
            }
        }
    }
}
