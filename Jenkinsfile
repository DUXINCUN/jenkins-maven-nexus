pipeline {
    agent none
    stages {
        stage('Build') {
    	    agent {
		docker {
       			image 'maven:3-alpine'
            		args '-v /root/.m2:/root/.m2'
		}
    	    }
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
	stage('Nexus') {
            agent any
            steps {
		nexusPublisher(nexusInstanceId: nexus3, 
			nexusRepositoryId: 'maven-releases', 
			packages: [ 
			[
			$class: 'MavenPackage',
			mavenAssesList: [
				[classifier: '',
					extension: '',
					filePath: './target/CurrencyConverter.war'
				]
			]
			mavenCoordinate: [
			artifactId: 'CurrencyConverter‘,
			groupId: ’sim',
			packaging: 'war', 
			version: '${BUILD_NUMBER}'
			]
			]  // end of packages
		])				
            }
        }
    }
}
