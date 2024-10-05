pipeline {
    agent any
    
    stages {
        stage('Clone') {
            steps {
              git branch: 'main', url: 'https://github.com/nivas-22/java-junit.git' 
            }      
        }
        stage('Build') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Unit Test') {
            steps {
                sh 'mvn test'
            }
        }
         stage('Integration  Test') {
        steps {
                sh 'mvn verify'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker build -t helloworld .'
                sh 'docker run -d -p 8082:8080 helloworld'
            }
        }
        
        stage('Upload Artifact') {
            steps {
                withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-credentials']]) {
                    sh 'aws s3 cp target/helloworld-servlet-1.0-SNAPSHOT.jar s3://nivascicd/'
                
}
}
}
}
