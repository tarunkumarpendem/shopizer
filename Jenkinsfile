pipeline{
    agent {
        label 'MVN3'
    }
    parameters{
        choice(name: 'Branch_to_Build', choices: ['master', 'develop', 'release'], description: 'selecting reuired branch')
        string(name: 'Maven_Goal', defaultValue: 'clean', description: 'selecting maven goal')
    }
    post{
        always{
            echo 'build completed'
        }
        failure{
            echo 'build failed'
            mail subject: 'Job is completed', 
                 body: """Job's done for $env.JOB_NAME
                                         $env.BUILD_NUMBER
                          \n clickhere:  $env.BUILD_URL""",
                 to: 'tarunkumarpendem22@gmail.com'
        }
        success{
            build success for "${env.JOB_NAME}"
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
        stage ('Artifactory configuration') {
            steps {
                rtMavenDeployer (
                    id: "Maven_1",
                    serverId: "https://tarun17.jfrog.io/",
                    releaseRepo: 'tarun-libs-release-local',
                    snapshotRepo: 'tarun-snapshot-release-local'
                )
            }
        }
        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: 'MVN-3.6.3', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: "${params.Maven_Goal}",
                    deployerId: "MAVEN_DEPLOYER"
                )
            }
        }
        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "Maven_1"
                )
            }
        }
    }
}