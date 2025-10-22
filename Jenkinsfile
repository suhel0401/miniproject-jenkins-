node {
    stage('Checkout') {
        git branch: 'dev', url: 'https://github.com/suhel0401/miniproject-jenkins-.git'
    }

    stage('Build') {
        sh 'mvn clean package'
        archiveArtifacts artifacts: 'target/*.war', fingerprint: true
    }

    stage('CQA') {
        withSonarQubeEnv('Suhel') {
            withCredentials([string(credentialsId: 'sonar', variable: 'SONAR_TOKEN')]) {
                sh 'mvn sonar:sonar -Dsonar.login=$SONAR_TOKEN'
            }
        }
    }
    stage ('Artifact') {
        nexusArtifactUploader artifacts: [[artifactId: 'loopwear-app', classifier: '', file: 'target/loopwear-app-1.0-SNAPSHOT.war', type: 'war']], credentialsId: 'nexus', groupId: 'com.loopwear', nexusUrl: '54.83.110.110:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'myrepo', version: '1.0-SNAPSHOT'
}
