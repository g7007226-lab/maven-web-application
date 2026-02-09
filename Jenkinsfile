pipeline {

agent any 

tools { maven "Suji" }
parameters {
  choice choices: ['master', 'QAT', 'test'], name: 'Branchname'
}

stages {
	stage ('check code') {
		steps  {
		 git branch: "${params.Branchname}", credentialsId: 'e0e91656-881b-4e6c-a045-0d113dff0754',
            url: 'https://github.com/g7007226-lab/maven-web-application/' }  }
	stage ('building package') {
		steps {
		sh "mvn clean package" } }
	stage ('publishing the app') {
    steps {
        deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '5f400706-e3d4-4ed2-a169-13b692484bc5', path: '', url: 'http://suji-1483923190.us-east-1.elb.amazonaws.com:8080')], war: 'target/maven-web-application.war'
    }
}
	}
}
