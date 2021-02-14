
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
                //sh 'rm -rf ${WORKSPACE}/remotepush && mkdir -p ${WORKSPACE}/remotepush'
                //sh 'cd remotepush'
                sh 'pwd'
                sh 'cp ${WORKSPACE}/build/libs/workspace.war .'
                sh 'git init'
                sh 'git checkout -b remote-repo'
                sh 'git add --all'
                sh 'git commit -m "first commit"'
                //sh 'git remote set-url origin https://github.com/duttamca/jenkinsbuildrepo.git'
                sh 'git remote add fakeorigin https://github.com/duttamca/jenkinsbuildrepo.git'
                sh 'git push --set-upstream fakeorigin remote-repo'
            }
         }
    }
}