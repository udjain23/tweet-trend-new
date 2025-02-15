pipeline {
    agent {
        node {
            label 'maven'
        }
    }

environment {
    PATH = "/opt/apache-maven-3.9.9/bin:$PATH"
}    

    stages {
        stage('build') {
            steps {
                echo "---------build started----------"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo "---------build completed----------"
            }
        }

        stage('test') {
            steps {
                echo "---------test started----------"
                sh 'mvn surefire-report:report'
                echo "---------test completed----------"
            }
        }

        stage('SonarQube analysis') {
        environment {    
         scannerHome = tool 'udjain_sonar-scanner'
        }
        steps{    
        withSonarQubeEnv('udjain_sonarqube-server') { // If you have configured more than one global server connection, you can specify its name
        sh "${scannerHome}/bin/sonar-scanner"
    }
    }
  }
}
}

