node {
    stage('SCM') {
        checkout scm
    }
    stage('SonarQube Analysis'){
        def mvn = tool 'maven';
        withSonarQubeEnv{
            sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=DevOps_HW2 -Dsonar.login=admin -Dsonar.password=DevOpsHw1"
        }
    }
    stage('Build JAR'){
        def mvn = tool 'maven'
        sh "${mvn}/bin/mvn package"
    }
    stage('Run Project'){
        // Run project
        sh "java -jar -Dserver.port=50001 target/spring-petclinic-3.0.0-SNAPSHOT.jar"

        // Wait for 5 minutes
        sh "sleep 300"
        
        // Send a termination signal to the Java process
        sh "killall java"
    }
}