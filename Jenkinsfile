pipeline {
  agent any

  stages {
      stage('Build Artifact') {
      steps {
        sh 'mvn clean package -DskipTests=true'
        archive 'target/*.jar' //so that they can be downloaded later test aa
      }
      }
    //--------------------------
    stage('Docker Build and Push') {
      steps {
        withCredentials([string(credentialsId: 'docker_hub_password_PA', variable: 'password')]) {
          sh 'sudo docker login -u tirtet -p $password'
          sh 'printenv'
          sh 'sudo docker build -t tirtet/devops-app:""$GIT_COMMIT"" .'
          sh 'sudo docker push tirtet/devops-app:""$GIT_COMMIT""'
        }
      }
    }


  }
}
