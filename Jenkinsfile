before = null
stage('Check before') {
	node {
		dir('before') {
			checkout scm
			sh 'cat date.txt'
			before = readFile 'date.txt'
		}
	}
}
stage('Update') {
	node {
		dir('update') {
			checkout scm
			sh 'git config --global user.email "you@example.com" && git config --global user.name "Your Name" && chmod go-rwx id_rsa && date > date.txt && git commit -am "test commit $(cat date.txt)" && GIT_SSH_COMMAND="ssh -o StrictHostKeyChecking=no -i id_rsa" git push git@github.com:leth/jenkins-pipeline-scm-test.git HEAD:master'
		}
	}
}
stage('Check after') {
	node {
		dir('after') {
			checkout scm
			sh 'cat date.txt'
			after = readFile 'date.txt'
			if (before != after) {
				error "dates do not match"
			}
		}
	}
}
