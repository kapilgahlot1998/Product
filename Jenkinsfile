pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "MAVEN_HOME"
    }

    stages {
        stage('Compile') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/kapilgahlot1998/Product.git'
                bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
        stage('Docker Build') {
            steps {
                bat "docker build -t  kapilgahlot98/micro_service:Product"
            }
        }
        stage('Docker Deploy') {
            steps {
                bat "docker push kapilgahlot98/micro_service:Product"
            }
        }
    }
}
