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
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" algorithm.sh'
            }
        }
        stage('Build') {
            steps {
                bat '"C:\\Program Files\\Git\\bin\\bash.exe" ./algorithm.sh'

                // Archive the report.txt file
                archiveArtifacts allowEmptyArchive: true,
                    artifacts: '*.txt',
                    fingerprint: true,
                    onlyIfSuccessful: true
            }
        }
    }
}

