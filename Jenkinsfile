pipeline {
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
        stage('Delivery') {
            steps {
                echo 'Build finished.'
            }
        }
	stage('Deploy') {
            agent any
            steps {
                 dir('ansible') {
                 ansiblePlaybook(playbook:'playbook.yml',inventory:'hosts')
                 }
            }
        }
    }
}
