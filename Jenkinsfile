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
    stage('Build JAR'){
        def mvn = tool 'maven'
        sh "${mvn}/bin/mvn package"
    }
    stage('Run Project'){
        sh "java -jar -Dserver.port=50000 target/spring-petclinic-3.0.0-SNAPSHOT.jar"
    }
}