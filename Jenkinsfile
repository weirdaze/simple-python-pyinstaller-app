pipeline {
    agent none 
    stages {
        stage("Fix the permission issue") {
            agent any
            steps {
                sh "sudo chown root:jenkins /var/run/docker.sock"
            }

        }
        stage('Build') { 
            agent {
                docker {
                    image 'python:2-alpine'
                }
            }
            steps {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py' 
                stash(name: 'compiled-results', includes: 'sources/*.py*') 
            }
        }
    }
}