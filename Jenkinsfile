pipeline {
    agent any 
    tools {
        maven 'local_maven'
    }

     environment {
        AWS_ACCESS_KEY_ID     = credentials('jenkins-aws-secret-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('jenkins-aws-secret-access-key')
    }      

    stages {
        stage('Build') {
            steps{
            echo 'build'
            }
        }
        stage('Test') {
            steps {
           echo 'test'
            }
        }
        stage('Publish') {
            steps {
                // sh 'mvn clean package -Dmaven.test.skip=true'
                sh 'mvn clean package'
            }
            post {
                success {
                    archiveArtifacts './aamir/target/*.jar'
                    sh 'aws configure set region ap-south-1'
                    sh 'aws s3 cp  ./aamir/target/*.jar s3://s3jenkinsaamir'
                }
            }
        }
    }
}
