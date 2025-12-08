pipeline { 
   agent { label 'slave20' }

    tools {
        jdk 'JDK17'
        maven 'maven'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'feature-1', url: 'https://github.com/Vinivinay52/Parcel-service.git'
            }
        }

        stage('Build') {
            steps {
                dir('parcel-service') {  // Move into folder where pom.xml exists
                    sh 'mvn clean package -DskipTests=false'
                }
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'parcel-service/target/*.jar', fingerprint: true
            }
        }

        stage('Run Application') {
            steps {
                dir('parcel-service') {
                    sh 'nohup mvn spring-boot:run > app.log 2>&1 &'
                    echo "Application started successfully"
                }
            }
        }
    }
}
