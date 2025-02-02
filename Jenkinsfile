pipeline {
    agent any

    environment {
        dockerHome = tool name: 'myDocker', type: 'ToolType'  // Ensure these tools are defined in Manage Jenkins > Global Tool Configuration
        mavenHome = tool name: 'myMaven', type: 'ToolType'    // Ensure these tools are defined in Manage Jenkins > Global Tool Configuration
        PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
    }

    stages {
        stage('Checkout') {
            steps {
                sh 'mvn --version'  // Correct shell command
                sh 'docker version' // Correct shell command
                echo "Build"
                echo "$PATH - PATH"  // Corrected usage of env variable
                echo "$BUILD_NUMBER - env.BUILD_NUMBER"  // Corrected usage of env variable
                echo "$BUILD_ID - env.BUILD_ID"          // Corrected usage of env variable
                echo "$JOB_NAME - env.JOB_NAME"          // Corrected usage of env variable
                echo "$BUILD_TAG - env.BUILD_TAG"        // Corrected usage of env variable
                echo "$BUILD_URL - env.BUILD_URL"        // Corrected usage of env variable
            }
        }

        stage('Compile') {
            steps {
                sh "mvn clean compile"  // Corrected by adding `sh`
            }
        }

        stage('Test') {
            steps {
                sh "mvn test"  // Corrected to ensure the command is executed
            }
        }

        stage('Integration Test') {
            steps {
                sh "mvn failsafe:integration-test failsafe:verify"  // Fixed the syntax for the failsafe plugin
            }
        }
    }
}
