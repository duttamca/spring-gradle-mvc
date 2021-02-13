

 pipeline {
   agent any
   stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'jenkins-user-github', url: 'https://github.com/duttamca/spring-gradle-mvc.git/']]])

            }
        }
        stage ('Build') {
        	steps {
        		sh './gradlew clean build'
        	}
         }
        stage ('Push to Remote ') {
            steps {
                sh 'mkdir -p ${WORKSPACE}/remotepush'
                sh 'cd ${WORKSPACE}/remotepush'
                sh 'git clone https://github.com/duttamca/jenkinsbuildrepo.git'
                sh 'cp ${WORKSPACE}/build/libs/workspace.war jenkinsbuildrepo/'
                sh 'cd ${WORKSPACE}/remotepush/jenkinsbuildrepo'
                sh 'git add --all'
                sh 'git commit -m "first commit"'
                sh 'git push'
            }
         }
    }
}