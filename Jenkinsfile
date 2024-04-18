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
                deploy adapters: [tomcat7(credentialsId: '47796aaf-d5eb-4048-afd0-af652a4ef6cb', path: '', url: 'http://localhost:8181/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}
