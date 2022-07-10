pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'python3 -m py_compile sources/add2vals.py sources/calc.py'
            }
        }
        stage('Test') {
            steps {
                sh 'pytest-3 --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
            }
            post {
                always {
                    junit 'test-reports/results.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                sh 'pyinstaller --onefile /home/cloud_user/github/simple-python-pyinstaller-app/sources/add2vals.py'
            }
            
            post {
                success {
                    archiveArtifacts 'dist/add2vals'
                }
            }
        }
    }
}
