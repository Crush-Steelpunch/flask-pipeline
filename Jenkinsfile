pipeline {
    agent any
    stages {
        stage('checkout') {
            steps {
		checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Crush-Steelpunch/to-do-example.git']]])
            }
        }
        withPythonEnv('python3.8.6') {
            steps {
		withPythonEnv ('python3.8.6'){
			sh "python3 -m pip install -r requirements.txt"
			sh "python3 create.py"
		}
>>>>>>> pyenv
            }
        }
        withPythonEnv('python3.8.6') {
            steps {
		sh "python3 -m pytest"
            }
        }
        withPythonEnv('python3.8.6') {
            steps {
		sh "python3 app.py"
            }
        }
    }
}
