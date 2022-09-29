pipeline{
	agent { label 'OPENJDK-11-MAVEN' }
	parameters{
		choice(name:'BRANCH_TO_BUILD',choices: ['REL_INI_1.0','main'],description:'branch to build')
		string(name: 'MAVEN_GOAL', defaultValue: 'package', description: 'maven goal') 
	}
	stages {
		stage ('vcs'){
			steps {
				git branch: "${params.BRANCH_TO_BUILD}", url: 'https://github.com/subramanyamgb/spring-petclinic.git'
			}
		}
		stage('build') {
			steps {
				sh "/opt/apache-maven-3.8.6/bin/mvn package ${params.MAVEN_GOAL}"
			}
		}
		stage('archive results') {
			steps {
				junit '**/surefire-reports/*.xml'
			}
		}
	}
}