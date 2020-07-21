pipeline {
  agent {
    label 'docker-dind-slave'
  }
  stages {
    stage('Build Docker Images') {
      steps {
        sh 'docker build -t electrum-wine-builder-img contrib/build-wine'
        sh 'docker build -t electrum-appimage-builder-img contrib/build-linux/appimage'
      }
    }

    stage('Build Windows Binary') {
      steps {
        sh "docker run --name electrum-wine-builder-cont -v /var/jenkins_home/worker/workspace/electrum_ci_jenkins:/opt/wine64/drive_c/electrum --rm --workdir /opt/wine64/drive_c/electrum/contrib/build-wine electrum-wine-builder-img ./build.sh"
        sh "docker run --name electrum-appimage-builder-cont -v /var/jenkins_home/worker/workspace/electrum_ci_jenkins:/opt/electrum --rm --workdir /opt/electrum/contrib/build-linux/appimage electrum-appimage-builder-img ./build.sh"
      }
    }
  }
}