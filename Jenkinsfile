pipeline {
    agent any
    options {
        buildDiscarder(logRotator(daysToKeepStr: '10', numToKeepStr: '10'))
        timeout(time: 12, unit: 'HOURS')
        timestamps()
    }
    stages {
        stage('Requirements') {
            steps {
                script {
                    if (isUnix()) {
                        sh('chmod +x ./algorithm.sh')
                    } else {
                        bat('algorithm.bat') // Windows equivalent
                    }
                }
            }
        }
        stage('Build') {
            steps {
                catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
                    sh('./algorithm.sh')
                }
                script {
                    if (fileExists('report.txt')) {
                        archiveArtifacts artifacts: '*.txt', fingerprint: true, onlyIfSuccessful: true
                    } else {
                        echo "No report.txt found to archive"
                    }
                }
            }
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check logs.'
        }
    }
}

