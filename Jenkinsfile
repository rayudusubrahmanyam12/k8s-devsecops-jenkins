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
  }
}