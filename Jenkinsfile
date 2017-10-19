pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                ansiColor('xterm') {
                    sh 'mvn clean test-compile'
                }
            }
        }
        stage('Verify') {
            steps {
                echo 'Verify..'
                ansiColor('xterm') {
                    sh 'mvn install'
                }
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
        stage('Verify with SNAPSHOT Parent') {
            steps {
                echo 'Running with latest parent SNAPSHOT...'
                ansiColor('xterm') {
                    sh 'mvn clean'
                    sh 'mvn versions:update-parent -DallowSnapshots=true'
                    sh 'mvn install'
                }
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }
}
