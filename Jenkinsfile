
stage('Check before') {
	node {
		dir('before') {
			checkout scm
			sh 'cat date.txt'
		}
	}
}
stage('Update') {
	node {
		dir('update') {
			checkout scm
			sh 'date > date.txt && git commit -am "test commit $(cat date.txt)" && GIT_SSH_COMMAND="ssh -i id_rsa" git push origin master'
		}
	}
}
stage('Check after') {
	node {
		dir('after') {
			checkout scm
			sh 'cat date.txt'
		}
	}
}