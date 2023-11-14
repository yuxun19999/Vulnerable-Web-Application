// testingtoek: sqp_f2aa90d6f3b318bd95f0648ed5f0d54c2b2a5d0b

sonar-scanner \
  -Dsonar.projectKey='OWASP' \
  -Dsonar.sources='.' \
  -Dsonar.host.url='http://localhost:9000' \
  -Dsonar.token='sqp_f2aa90d6f3b318bd95f0648ed5f0d54c2b2a5d0b'


pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/yuxun19999/Vulnerable-Web-Application.git'
            }
        }

        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                    def scannerHome = tool 'SonarQube'
                    withSonarQubeEnv('SonarQube') {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=OWASP -Dsonar.sources=." +
                            " -Dsonar.host.url=http://localhost:9000"

                    }
                }
            }
        }
    }

    post {
        always {
            recordIssues enabledForFailure: true, tool: sonarQube()
        }
    }
}

