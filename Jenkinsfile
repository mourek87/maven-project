pipeline {
    agent any

    parameters {
         string(name: 'tomcat_dev', defaultValue: '172.17.0.6', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '172.17.0.7', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
				withCredentials([usernamePassword(credentialsId: '1e22f4b2-fe72-4408-b34b-1f9abe1e47b3', passwordVariable: 'tomcat', usernameVariable: 'tomcat')]) {
    sh "scp **/target/*.war tomcat@${params.tomcat_dev}:/usr/local/tomcat/webapps"
}
                    }
                }

                stage ("Deploy to Production"){
			steps {  
				withCredentials([usernamePassword(credentialsId: '1e22f4b2-fe72-4408-b34b-1f9abe1e47b3', passwordVariable: 'tomcat', usernameVariable: 'tomcat')]) {
    sh "scp **/target/*.war tomcat@${params.tomcat_prod}:/usr/local/tomcat/webapps"
}
			}
                }
            }
        }
    }
}
