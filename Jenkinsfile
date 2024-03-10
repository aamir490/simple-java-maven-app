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
                sh 'mvn package'
            }
            post {
                success {
                    //archiveArtifacts './web/target/*.war'
                    sh 'aws configure set region ap-south-1'
                    sh 'aws s3 cp ./web/target/*.war s3://s3jenkinsaamir'
                }
            }
        }
    }
}
