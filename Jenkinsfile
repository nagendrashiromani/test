pipeline {
  agent any
  stages {
	stage('checkout'){
		checkout scm
		steps{
			script{
				if (lastCommitIsVersionCommit()) {
					currentBuild.result = 'ABORTED'
					error('Last commit bumped the version, aborting the build to prevent a loop.')
				} else {
					echo('Last commit is not a bump commit, job continues as normal.')
				}
			}
		}
	}
  
    stage('First Stage') {
      steps {
        parallel(
          "First Stage": {
            sh 'echo "Hello world"'
            
          },
          "Parallel First": {
            sh 'echo "parallel first step"'
            
          }
        )
      }
    }
    stage('Second Stage') {
      steps {
        sh 'echo "second step"'
      }
    }
  }
}

private boolean lastCommitIsVersionCommit() {
		lastCommit = sh([script: 'git log -1', returnStdout: true])
		if (lastCommit.contains("Verion changed")) {
			return true
		} else {
			return false
		}
	}