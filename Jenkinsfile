pipeline {
    agent any

    environment {
        SONARQUBE_SERVER = 'sonarqube' // Name from Jenkins SonarQube configuration
    }

    stages {
        stage('Build') {
            steps {
                // Compile the project and skip tests
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Run SonarQube scan using Jenkins credentials
                withSonarQubeEnv(SONARQUBE_SERVER) {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=java-project -Dsonar.host.url=http://192.168.1.157:9000'
                }
            }
        }
        stage('Deploy Artifact to Nexus') {
    steps {
        sh "mvn deploy -DskipTests --settings /opt/maven-config/settings.xml"
    }
}
    }
}

