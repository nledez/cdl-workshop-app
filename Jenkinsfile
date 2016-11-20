stage('build & unit tests') {
	node('build') {
		sleep 1
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
	node('build') {
		sleep 1
	}
}

stage('manual-approval') {
	input 'Deploy in production?'
}
