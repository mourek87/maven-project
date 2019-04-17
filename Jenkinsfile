def version = 'init'
pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: '35.166.210.154', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '34.209.233.6', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }
    
	stages{   
		stage('Parallel'){
			parallel {
				stage('Build'){
					steps {
						sh 'echo ${version}'
						sh 'git describe --tags | cut -c 1-4'
						script {
							version = sh(
							script: "git describe --tags | cut -c 1-4",
							returnStdout: true,
						  ) 
						}                       
						sh 'echo ${version}'
					}
				}
				stage('Echo'){
					steps {
						sh 'echo ${BUILD_NUMBER}'
						sh 'echo ${BUILD_ID}'
						sh 'echo ${BUILD_URL}'
						sh 'echo ${NODE_NAME}'
						sh 'echo ${JOB_NAME}'
						sh 'echo ${BUILD_TAG}'
						sh 'echo ${JENKINS_URL}'
						sh 'echo ${EXECUTOR_NUMBER}'
						sh 'echo ${JAVA_HOME}'
						sh 'echo ${WORKSPACE}'
						sh 'echo ${SVN_REVISION}'
						sh 'echo ${CVS_BRANCH}'
						sh 'echo ${GIT_COMMIT}'
						sh 'echo ${GIT_URL}'
						sh 'echo ${GIT_BRANCH}'
					}
				}
			}
		}
	}
}
