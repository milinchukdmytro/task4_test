pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/milinchukdmytro/task4_test.git', branch: 'main'
            }
        }
        
        stage('Build') {
            steps {
                script {
                    try {
                        bat '"D:\\Visual Studio\\MSBuild\\Current\\Bin\\MSBuild.exe" test_repos.sln /p:Configuration=Debug /p:Platform=x64 /m'
                    } catch (Exception e) {
                        echo "Build error: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Pipeline stopped due to build failure.")
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    try {
                        bat '"D:\\kursovasysprog\\Task4_test\\x64\\Debug\\test_repos.exe"'
                    } catch (Exception e) {
                        echo "Test error: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        error("Pipeline stopped due to test execution failure.")
                    }
                }
            }
        }
    }

    post {
        always {
            //cleanWs()
            echo "1"
        }
        
        failure {
            echo "Pipeline failed. Check logs to fix the issues."
        }
        
        success {
            echo "Pipeline completed successfully!"
        }
    }
}
