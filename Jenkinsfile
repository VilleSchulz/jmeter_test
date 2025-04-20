pipeline {
    agent any

    tools {
        maven 'Maven3' // Make sure this is correctly defined in Jenkins global tool config
    }

    environment {
        JMETER_HOME = 'C:\\Tools\\apache-jmeter-5.6.3'
        PATH = "${JMETER_HOME}\\bin;${env.PATH}"
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Non-Functional Test') {
            steps {
                bat 'jmeter -n -t tests/performance/demo.jmx -l result.jtl'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'result.jtl', allowEmptyArchive: true
            perfReport sourceDataFiles: 'result.jtl'
        }
    }
}
