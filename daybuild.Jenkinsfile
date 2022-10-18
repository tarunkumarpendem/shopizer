pipeline {
    agent {label 'MVN3'}
    triggers {
        pollSCM('30 16 * * *')
    }
    stages {
        stage('vcs') {
            steps {
                git  url: 'git@github.com:tarunkumarpendem/shopizer.git',  
                     branch: 'promoter-daybuild'       
            }
        }
        stage('merge') {
            steps {
                sh 'pwd'
                sh 'ls'
                sh 'git checkout develop'
                sh 'git checkout release'
                sh 'git branch -a'
                sh 'git merge develop --no-ff'
                sh 'git log --oneline --graph --decorate --all'
                sh 'git push -u origin release'
            }
        }
    }
}