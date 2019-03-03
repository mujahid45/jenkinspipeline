pipeline {
    agent any
	tools {
	  maven 'localmaven'
	  }

stages{
        stage('Build'){
		  
            steps {
                   sh "mvn clean package"
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
                        sh "cp  **/*.war /opt/tomcat/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        sh "cp  **/*.war /opt/tomcat_prod/webapps"
                    }
                }
            }
        }
    }
}
