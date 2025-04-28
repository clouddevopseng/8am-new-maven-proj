pipeline {
    agent any
    environment {
        // JFrog credentials and URL
        JFROG_URL = 'https://trialhbtl8e.jfrog.io'
        JFROG_USER = 'jfrog'
        JFROG_PASSWORD = 'Jfrog123'

        // Tomcat server details
        TOMCAT_URL = 'http://13.234.225.88:8080'
        TOMCAT_USER = 'dev'
        TOMCAT_PASSWORD = 'dev123'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'dev', url: 'https://github.com/clouddevopseng/8am-new-maven-proj.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    sh 'mvn clean package'
                }
            }
        }
        stage('Artifact Upload') {
            steps {
                script {
                    rtUpload(
                        serverId: 'artifactory-server',
                        spec: '''{
                            "files": [
                                {
                                    "pattern": "target/*.war",
                                    "target": "genricproject-generic-local/"
                                }
                            ]
                        }'''
                    )
                }
            }
        }
		stage('Download Artifact') 
		{
            steps {
                 script {
                    sh """
                       curl -u ${JFROG_USER}:${JFROG_PASSWORD} \
                       -O ${JFROG_URL}/artifactory/genricproject-generic-local/artifacts-0.0.1-SNAPSHOT.war
                       """
        }
    }
}
        stage('Deploy to Tomcat') {
            steps {
                script {
                    // Deploy the WAR file to Tomcat server
                    def artifactUrl = "${JFROG_URL}/artifactory/genricproject-generic-local/artifacts-0.0.1-SNAPSHOT.war"
                    sh """
                        curl -u ${TOMCAT_USER}:${TOMCAT_PASSWORD} \
                        --upload-file artifacts-0.0.1-SNAPSHOT.war \
                        ${TOMCAT_URL}/deploy?path=/artifacts-0.0.1-SNAPSHOT
                    """
                }
            }
        }
    }
}
