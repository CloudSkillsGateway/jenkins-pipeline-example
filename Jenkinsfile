pipeline {
    agent any
    tools {
        maven "MAVEN"  // Ensure Maven is configured in Jenkins' Global Tool Configuration
        jdk "JDK"      // Ensure JDK is configured in Jenkins' Global Tool Configuration
    }
    stages {
        stage('Initialize'){
            steps{
                echo "PATH = ${M2_HOME}/bin;${PATH}"  // Adjust path separator for Windows
                echo "M2_HOME = ${env.M2_HOME}"      // Use the correct environment variable for Maven
            }
        }
        stage('Build') {
            steps {
                dir("C:\\Jenkins\\workspace\\demopipelinetask\\my-app") { // Use Windows path here
                    bat 'mvn -B -DskipTests clean package'  // Use bat instead of sh for Windows
                }
            }
        }
    }
    post {
        always {
            junit(
                allowEmptyResults: true,
                testResults: '**/test-reports/*.xml' // Correct path to test reports
            )
        }
    }
}
