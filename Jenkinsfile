pipeline {
  agent any

  stages {
      stage('Build Artifact') {
            steps {
              sh "mvn clean package -DskipTests=true"
              archive 'target/*.jar' //so that they can be downloaded later
            }
        }   
    stage('Unit Tests - JUnit and JaCoCo') {
      steps {
        sh "mvn test"
        jacoco execPattern: 'target/jacoco.exec'
      }
    } 

    stage('Docker Build and Push') {
      steps {
        withDockerRegistry([credentialsId: "docker-hub", url: ""]) {
          sh 'printenv'
          sh 'docker build -t rayudusubrahmanyam12/numeric-app:""$GIT_COMMIT"" .'
          sh 'docker push rayudusubrahmanyam12/numeric-app:""$GIT_COMMIT""'
        }
      }
    } 
  }
}