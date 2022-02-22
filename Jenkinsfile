pipeline {
    agent any
    stages {
        stage('checkout') {
            steps {
		checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Crush-Steelpunch/to-do-example.git']]])
            }
        }
        stage('environment and deps and init database') {
            steps {
		withPythonEnv ('python3.8.6'){
			sh "python3 -m pip install -r requirements.txt"
			sh "python3 create.py"
		}
            }
        }
        stage('testing') {
            steps {
                sh "source venv/bin/activate; \
		python3 -m pytest"
            }
        }
        stage('run app') {
            steps {
                sh "source venv/bin/activate; \
		python3 app.py"
            }
        }
    }
}
