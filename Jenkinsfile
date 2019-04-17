pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: '35.166.210.154', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '34.209.233.6', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }
    
    environment {
            version = 'init'
        }
    
stages{   
    stage('Build'){
            steps {
                sh 'echo ${version}'
                script {
                    version = sh(
                    script: "git describe --tags | cut -c 1-4",
                    returnStdout: true,
                  ) 
                }                       
                sh 'echo ${version}'
            }
        }
    }
}
