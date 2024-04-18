pipeline {
    agent any
    tools {
        // Define a custom Maven tool named 'local maven' pointing to the installed Maven in Jenkins
        maven 'local_maven'
    }
    stages {
        stage('Build') {
            steps {
                // Use 'bat' instead of 'sh' to execute commands on Windows
                bat 'mvn clean package'
            }
            post {
                success {
                    echo "Archiving the Artifacts"
                    archiveArtifacts '**/target/*.war'
                }
            }
        }
        stage('Deploy to Tomcat server') {
            steps {
                deploy adapters: [tomcat7(credentialsId: '2054cb92-138b-42c4-8b4f-d46df5d050a3', path: '', url: 'http://localhost:8181')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
