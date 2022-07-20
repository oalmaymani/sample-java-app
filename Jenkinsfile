pipeline {

    agent any

    stages {

        stage('Build'){
            steps {
                sh "mvn clean"

                sh "mvn compile"
            }
        }

        stage('Test'){
            steps {
                sh "mvn test"
            }

            post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }

        stage('sonar scan'){
            steps {
              sh "mvn clean verify sonar:sonar \
  -Dsonar.projectKey=osaid-almaymani \
  -Dsonar.host.url=http://54.226.50.200 \
  -Dsonar.login=sqp_9552531c828fa179f8467abca9bf2072aad1fc8a"
            }
        }

        stage('Package'){
            steps {
                
                sh "mvn package"
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.war', followSymlinks: false
                }
            }
        }

    }

}