node {
    stage('Checkout') {
        git branch: 'dev', url: 'https://github.com/suhel0401/miniproject-jenkins-.git'
    }

    stage('Build') {
        sh 'mvn clean package'
        archiveArtifacts artifacts: 'target/*.war', fingerprint: true
    }
}
