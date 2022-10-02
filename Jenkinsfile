pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
       stage('Build Artifact - Maven') {
           steps {
               sh "mvn clean package -DskipTests=true"
               archive 'target/*.jar'
       }
     }
      stage('Unit Tests - JUnit and JaCoCo') {
          steps {
               sh "mvn test"
      }
    }
     stage('SonarQube - SAST') {
         steps {
       withSonarQubeEnv('SonarQube') {
          sh "mvn sonar:sonar \
		              -Dsonar.login=admin \
	 	              -Dsonar.password=louay"
      }
        timeout(time: 2, unit: 'MINUTES') {
          script {
            waitForQualityGate abortPipeline: true
          }
       }
      }
     }
    }
}
