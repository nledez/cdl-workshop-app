stage('build & unit tests') {
	node('build') {
		mvnHome = tool 'M3'
		checkout scm
		sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
		stash includes: 'target/simple-app-1.0-SNAPSHOT.jar', name: 'jar'
	}
}

stage('integration-tests') {
	node('build') {
		sleep 1
	}
}

stage('acceptance-tests') {
	parallel (
			"chrome" : {
				node('test') {
					sh "sleep 10"
				}
			},
			"edge" : {
				node('test') {
					sh "sleep 10"
				}
			},
			"firefox" : {
				node('test') {
					sh "sleep 10"
				}
			}
		 )
}

stage('staging') {
	node('ssh') {
		unstash 'jar'
		sh "ls -l target"
	}
}

stage('manual-approval') {
	input 'Deploy in production?'
}

stage('production') {
	node('ssh') {
		unstash 'jar'
		sh "ls -l target"
	}
}
