

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
                sh 'mkdir -p ${WORKSPACE}/remotepush && cp ${WORKSPACE}/build/libs/workspace.war ${WORKSPACE}/remotepush/'
                sh 'cd ${WORKSPACE}/remotepush'
                sh 'git init'
                sh 'git add --all'
                sh 'git commit -m "pushing to remote repo"'
                sh 'git branch -M main'
                sh 'git remote add origin https://github.com/duttamca/jenkinsbuildrepo.git'
                sh 'git push -u origin main'
            }
         }
    }
}