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
                sh 'pytest --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
            }
            post {
                always {
                    junit 'test-reports/results.xml'
                }
            }
        }
         stage('Deliver') {
            steps {
                sh 'pyinstaller --onefile /home/shanu/github/example/sources/add2vals.py'
            }
            post {
                success {
                    archiveArtifacts 'dist/add2vals'
                }
            }
        }
         stage('Deploy') {
            steps {                 
                sh 'scp -r /var/lib/jenkins/workspace/add2values/dist cloud_user@9e2c2aef731c.mylabserver.com:/var/tmp'
            }
        }   
    }
}
