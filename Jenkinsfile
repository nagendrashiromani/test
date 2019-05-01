pipeline {
  agent any
	//triggers{
		//cron('H H 1 1 *')
	//}
  stages {
	stage('checkout'){
		steps{
			checkout scm
			//git url: 'https://github.com/nagendrashiromani/test.git', credentialsId: 'c703ef9e-f396-4c67-84d4-80fd8ac1272c'
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
