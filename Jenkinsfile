pipeline {
        agent any

        parameters {
                choice choices: ['slave1', 'slave2'], name: 'ENVIRONMENT'
}

        stages {
      	stage('Checkout SCM') {
      		steps {
      			checkout scm
      		}
      	}
      	stage('Build') {
      		steps {
      			sh '/home/therecker/DevOps/Maven/apache-maven-3.9.6/bin/mvn install'
      		}
      	}
      	stage('Deployment on Slaves') {
      		steps {
      			script {
      				if ( env.ENVIRONMENT == 'slave1' ) {
      					sh "sshpass -p 'redhat' scp target/multi-slave.war admin@172.17.0.2:/home/admin/apache-tomcat-9.0.86/webapps"
      				}
      				elif ( env.ENVIRONMENT == 'slave2' ) {
      					sh "sshpass -p 'redhat' scp target/multi-slave.war admin@172.17.0.3:/home/admin/apache-tomcat-9.0.86/webapps"
      				}
      				fi
      			}
      		}
      	}
      }
