pipeline {
    agent any
    stages {
        stage('Test') {
            steps {
                dir('/Users/truyen.nguyen/Downloads/ci-samples') {
                    sh '''
                        echo "Current directory:"
                        pwd
                        echo "Listing files:"
                        ls -l
                        echo "Running Docker container:"
                        docker run --platform linux/amd64 -t --rm -v "$(pwd)":/tmp/project katalonstudio/katalon katalonc.sh -projectPath=/tmp/project -browserType=Chrome -retry=0 -statusDelay=15 -testSuitePath="Test Suites/TS_RegressionTest" -apiKey=8389077c-ca38-4148-ad5a-0f60e417dd92
                        echo "Docker container finished. Listing files again:"
                        ls -l /tmp/project/Reports
                    '''
                }
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'Reports/**/*.*', fingerprint: true
            junit 'Reports/**/JUnit_Report.xml'
        }
        failure {
            script {
                echo 'Test failed. Checking the contents of the Reports directory...'
                sh 'ls -l /Users/truyen.nguyen/Downloads/ci-samples/Reports'
            }
        }
    }
}
