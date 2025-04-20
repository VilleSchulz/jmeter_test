pipeline {
    agent any

    tools {
        maven 'Maven3' // Ensure this is defined in Jenkins Global Tools config
    }

    environment {
        JMETER_HOME = 'C:\\apache-jmeter-5.5' // ✅ Replace with the actual path to your JMeter installation
        PATH = "${JMETER_HOME}\\bin;${env.PATH}" // Add JMeter to system path
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
        }pipeline {
             agent any

             tools {
                 maven 'Maven3' // Adjust to your configured Maven tool name
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

    }
}
