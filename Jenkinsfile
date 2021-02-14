
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
            sh '''
                //rm -rf ${WORKSPACE}/remotepush && mkdir -p ${WORKSPACE}/remotepush
                //sh 'cd remotepush'
                pwd
                cp ${WORKSPACE}/build/libs/workspace.war .
                git init
                git checkout -b remote-repo
                git add --all
                git commit -m "first commit"
                git remote add fakeorigin https://github.com/duttamca/jenkinsbuildrepo.git
                git push --set-upstream fakeorigin remote-repo
            '''
            }
         }
    }
}