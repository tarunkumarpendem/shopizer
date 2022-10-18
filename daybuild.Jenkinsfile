pipeline {
    agent {label 'MVN3'}
    //triggers {
      //  pollSCM('5 * * * *')
    //}
    stages {
        stage('vcs') {
            steps {
                git  url: 'https://github.com/longflewtinku/shopizer.git'  
                     branch: 'promoter-daybuild'       
            }
        }
        stage('merge') {
            steps {
                sh 'pwd'
                sh 'ls'
                //sh 'git checkout release'
                //sh 'git merge develop --no-ff'
            }
        }
    }
}