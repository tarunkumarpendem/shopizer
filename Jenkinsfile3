pipeline{
    agent {
        label 'MVN3'
    }
    parameters{
        choice(name: 'Branch_to_Build', choices: ['master', 'develop', 'release'], description: 'selecting reuired branch')
    }
    post{
        always{
            echo 'build completed'
        }
        failure{
            echo 'build failed'
        }
        success{
            echo 'build success'
        }
    }
    triggers{
        pollSCM('30 17 * * *')
    }
    stages{
        stage('clone'){
            steps{
                git url: 'https://github.com/tarunkumarpendem/shopizer.git',
                    branch: "${params.Branch_to_Build}"
            }
        }
        stage('install'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('archiving-artifacts'){
            steps{
                archiveArtifacts artifacts: '**/target/*.jar', followSymlinks: false
            }
        }
        stage('junit_reports'){
            steps{
                junit '**/surefire-reports/*.xml'
            }
        }
    }
}