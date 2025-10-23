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

    stage('Artifact') {
      nexusArtifactUploader artifacts: [[artifactId: 'loopwear-app', classifier: '', file: 'target/loopwear-app-1.0.war', type: 'war']], credentialsId: 'nexus', groupId: 'com.loopwear', nexusUrl: '13.218.133.0:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'Myrepo', version: '1.0'
    }

    stage('Deploy') {
        deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'tomcat', path: '', url: 'http://184.72.199.97:8080')], contextPath: 'loopwear', war: 'target/*.war'
    }
}
