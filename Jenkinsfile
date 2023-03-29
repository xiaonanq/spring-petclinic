node {
    stage('SCM') {
        checkout scm
    }
    stage('SonarQube Analysis'){
        def mvn = tool 'maven';
        withSonarQubeEnv{
            sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=sonarqube -Dsonar.login=admin -Dsonar.password=DevOpsHw1"
        }
    }
}