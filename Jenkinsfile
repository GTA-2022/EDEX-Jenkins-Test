pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Nachricht von GTA!'
        sh 'sh run_build_scropt.sh'
      }
    }

    stage('Linux-Tests') {
      parallel {
        stage('Linux-Tests') {
          steps {
            echo 'Linux-Tests-Werden ausgeführt!'
          }
        }

        stage('Windows-Tests') {
          steps {
            echo 'Windows-Tests werden ausgeführt'
          }
        }

      }
    }

    stage('DEPLOY-PRE-Produktion') {
      steps {
        echo 'Die Phase "Deployen" wurde erreicht!'
        input 'Das Deployen beginnt'
      }
    }

    stage('Produktions-Deploy') {
      steps {
        echo 'Das Deployen in der Produktion hat begonnen!'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
    }

    failure {
      mail(to: 'YOUR EMAIL ADDRESS', subject: "Failed Pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
    }

  }
}