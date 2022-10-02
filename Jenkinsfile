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
        stage('Git') {
           steps {
		echo "Getting project from Git";
                git "https://github.com/louaymed/timesheet-ci.git";
            }
	}
        
     stage('SonarQube') {
       steps {
        sh "mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=louay"
      }
     }
  stage('Docker Build and Push') {
       steps {
         withDockerRegistry([credentialsId: "docker-hub", url: ""]) {
           sh 'printenv'
           sh 'sudo docker build -t louaymed/timesheet-ci:""$GIT_COMMIT"" .'
           sh 'docker push louaymed/timesheet-ci:""$GIT_COMMIT""'
         }
       }
    }
    }
}
