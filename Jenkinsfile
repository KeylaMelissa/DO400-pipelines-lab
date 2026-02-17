pipeline {
    agent any
    
    parameters {
        booleanParam(name: "RUN_INTEGRATION_TESTS", defaultValue: true)
    }
    stages {
        stage('Test') {
            parallel {
                stage('Unit tests') {
                    steps {
                        sh 'chmod +x mvnw'
                        sh './mvnw test -DtestGroups=unit'
                    }
                }
                stage('Integration tests') {
                    when { expression { return params.RUN_INTEGRATION_TESTS } }
                    steps {
                        sh 'chmod +x mvnw'
                        sh './mvnw test -DtestGroups=integration'
                    }
                }
            }
        }
        stage('Build') {
            steps {
                script {
                    try {
                        sh './mvnw package -D skipTests'
                    } catch (ex) {
                        echo "Error while generating JAR file"
                        throw ex
                    }
                }
            }
        }
    }
}