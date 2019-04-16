pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: '35.166.210.154', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '34.209.233.6', description: 'Production Server')
         string(defaultValue: "", description: '', name: 'APP_VERSION')
    }

    def version = env.APP_VERSION
    
    triggers {
         pollSCM('* * * * *')
     }

stages{
        stage('Build'){
            steps {
                version = sh(script: "git describe --tags | cut -c 1-4", returnStdout: true).trim()            
                sh 'echo ${version}'
            }
        }
    }
}
