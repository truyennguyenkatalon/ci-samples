pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                dir('/Users/truyen.nguyen/Downloads/ci-samples'){
                    sh 'docker run -t --rm -v "$(pwd)":/tmp/project katalonstudio/katalon katalonc.sh -projectPath=/tmp/project -browserType="Chrome" -retry=0 -statusDelay=15 -testSuitePath="Test Suites/TS_RegressionTest" -apiKey="5e688284-405a-42d1-a07a-1a68cec8422d" -orgID=301267'
                }
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'Reports/**/*.*', fingerprint: true
            junit 'Reports/**/JUnit_Report.xml'
        }
    }
}
