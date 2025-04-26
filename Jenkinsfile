pipeline {
    agent any
    tools {
        maven "MAVEN"  // Ensure Maven is configured in Jenkins' Global Tool Configuration
        jdk "jdk17"      // Ensure JDK is configured in Jenkins' Global Tool Configuration
    }
    stages {
        stage('Initialize'){
            steps{
                echo "M2_HOME = ${env.M2_HOME}"  // Use the correct environment variable for Maven
                echo "PATH = ${M2_HOME}/bin;${PATH}"  // Adjust path separator for Windows
            }
        }
        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        // For Unix-based nodes (Linux, macOS)
                        dir("my-app") {
                            sh 'mvn -B -DskipTests clean package'  // Use sh for Unix-based systems
                        }
                    } else {
                        // For Windows nodes
                        dir("C:\\Jenkins\\workspace\\demopipelinetask\\my-app") {
                            bat 'mvn -B -DskipTests clean package'  // Use bat for Windows nodes
                        }
                    }
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
