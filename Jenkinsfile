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
        withCredentials([string(credentialsId: 'docker-hub-password-PA', variable: 'DOCKER_HUB_PASSWORD')]) {
          sh 'sudo docker login -u tirtet -p $DOCKER_HUB_PASSWORD'
          sh 'printenv'
          sh 'sudo docker build -t tirtet/devops-app:""$GIT_COMMIT"" .'
          sh 'sudo docker push tirtet/devops-app:""$GIT_COMMIT""'
        }
      }
    }


  }
}
