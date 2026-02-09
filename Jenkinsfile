pipeline {
agent { label 'slaves' }
tools {
    maven "Suji" } // maven3.9.12 version configured as Suji
options {
  timestamps ()
      buildDiscarder logRotator(artifactDaysToKeepStr: '5', artifactNumToKeepStr: '5', daysToKeepStr: '5', numToKeepStr: '5')
}

stages {
    
stage('check out code') {
steps {
 git credentialsId: 'e0e91656-881b-4e6c-a045-0d113dff0754',
            url: 'https://github.com/g7007226-lab/maven-web-application'
}
}

stage('building package'){
steps {
sh "mvn clean package"
}
}

stage('creating report'){
steps {
        withSonarQubeEnv('SonarQube') {
            sh "mvn sonar:sonar"
}
}
}
/*
stage ('storing artifacats') {
steps {
sh "mvn deploy"
}
} */
stage ('publishing the app'){
    steps {
        deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: '5f400706-e3d4-4ed2-a169-13b692484bc5', path: '', url: 'http://suji-1483923190.us-east-1.elb.amazonaws.com:8080')], war: 'target/maven-web-application.war'
    }
} 
}
}
