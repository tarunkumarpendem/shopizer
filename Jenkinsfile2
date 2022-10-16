pipeline{
    agent {
        label 'MVN3'
    }
    triggers{
        pollSCM('* * * * *')
    }
    stages{
        stage('clone'){
            steps{
                git url: 'https://github.com/tarunkumarpendem/shopizer.git',
                    branch: 'develop'
            }
        }
        stage('build'){
            steps{
                sh 'mvn package'
            }
        }
        stage('archive'){
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