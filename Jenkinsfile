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
    }
}
