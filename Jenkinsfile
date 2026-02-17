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
                        sh './mvnw test -DtestGroups=unit'
                    }
                }
                stage('Integration tests') {
                    when { expression { return params.RUN_INTEGRATION_TESTS } }
                    steps {
                        sh './mvnw test -DtestGroups=integration'
                    }
                }
            }
        }
    }
}