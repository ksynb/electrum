pipeline {
  agent {
    label 'docker-dind-slave'
  }
  stages {
    stage('Build Docker Images') {
      steps {
        checkout scm
        sh 'docker build --no-cache -t electrum-wine-builder-img contrib/build-wine'
        sh 'docker build --no-cache -t electrum-appimage-builder-img contrib/build-linux/appimage'
      }
    }

    stage('Build Windows Binary') {
      steps {
        sh "docker run --name electrum-wine-builder-cont -v ./:/opt/wine64/drive_c/electrum --rm --workdir /opt/wine64/drive_c/electrum/contrib/build-wine electrum-wine-builder-img ./build.sh"
        sh "docker run --name electrum-appimage-builder-cont -v ./:/opt/electrum --rm --workdir /opt/electrum/contrib/build-linux/appimage electrum-appimage-builder-img ./build.sh"
      }
    }
  }
}