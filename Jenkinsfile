node {
    stage('Checkout') {
        git branch: 'dev', url: 'https://github.com/suhel0401/miniproject-jenkins-.git'
    }

    stage('Build') {
        sh 'mvn clean package'
        archiveArtifacts artifacts: 'target/*.war', fingerprint: true
    }

    stage('CQA') {
        withSonarQubeEnv('MySonarQubeServer') {
            withCredentials([string(credentialsId: 'sonarqube', variable: 'SONAR_TOKEN')]) {
                sh 'mvn sonar:sonar -Dsonar.login=$SONAR_TOKEN'
            }
        }
    }
}
