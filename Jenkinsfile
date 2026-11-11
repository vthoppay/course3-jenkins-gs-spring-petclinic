pipeline {
    agent any

    stages {
        stage("build")
        {
            steps{
           sh "./mvnw package -Djacoco.version=0.8.12"
        }
        }
        stage("capture"){
            steps{
            archiveArtifacts artifacts: '**/target/*.jar', followSymlinks: false
            }
        }
        stage ("code coverage")
        {
            steps{
            recordCoverage(tools: [[pattern: '**/target/site/jacoco/**.xml']])
            }
        }
    }
    post
{
    always
    {
    emailext body: '', recipientProviders: [developers()], subject: '"${BUILD_URL}"', to: 'always@foo.bar'
    }

}
}

