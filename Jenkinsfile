pipeline {
    agent any

    tools {
        maven 'Maven3' // Make sure "Maven3" is configured in Jenkins > Global Tool Configuration
    }

    environment {
        JMETER_HOME = 'C:\\apache-jmeter-5.5\\bin' // Adjust this to your JMeter installation path
        PATH = "${env.JMETER_HOME};${env.PATH}"
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
