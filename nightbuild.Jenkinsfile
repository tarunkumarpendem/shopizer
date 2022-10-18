pipeline {
    agent {label 'MVN3'}
    triggers {
        pollSCM('30 17 * * *')
    }
    stages {
        stage('vcs') {
            steps {
                git  url: 'https://github.com/tarunkumarpendem/shopizer.git',  
                     branch: 'promoter-build'       
            }
        }
        stage('build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('archive_artifacts'){
            steps{
                archiveArtifacts artifacts: '**/target/*.jar', followSymlinks: false
            }
        }
        stage('junit'){
            steps{
                junit '**/surefire-reports/*.xml'
            }
        }
    }
}