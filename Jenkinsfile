node {
    stage('SCM') {
        checkout scm
    }
    stage('SonarQube Analysis'){
        def mvn = tool 'maven';
        withSonarQubeEnv{
            sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=DevHW2 -Dsonar.login=sqp_020e1033c08debc77a9ad7679e48052c4f221947"
        }
    }
    stage('Build JAR'){
        def mvn = tool 'maven'
        sh "${mvn}/bin/mvn package"
    }
    stage('Run Project'){
        // Run project
        sh "java -jar -Dserver.port=50001 target/spring-petclinic-3.0.0-SNAPSHOT.jar"
    }
    stage('Run Project 5 mins'){
        // Wait for 5 minutes
        sh "sleep 300"
    }
    stage('Kill Project'){
        // Send a termination signal to the Java process
        sh "killall java"
    }
}