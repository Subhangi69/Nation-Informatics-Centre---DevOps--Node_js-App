pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-2'
        AWS_ACCESS_KEY_ID = credentials('AKIAQKGGW7HMZF3OSE2N')  // Replace with your credential ID
        AWS_SECRET_ACCESS_KEY = credentials('AKIAQKGGW7HMZF3OSE2N') // Replace with your credential ID
        APPLICATION_NAME = 'Nodejs'
        ENVIRONMENT_NAME = 'Nodejs-env'
        S3_BUCKET = 'elasticbeanstalk-us-east-2-006095271778'
        SOURCE_BUNDLE_NAME = 'node_modules.zip'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Subhangi69/Nation-Informatics-Centre---DevOps--Node_js-App']])
            }
        }

        stage('Build') {
            steps {
                script {
                    sh 'npm install'
                    sh 'npm test'
                }
            }
        }

        stage('Package') {
            steps {
                script {
                    sh "zip -r $SOURCE_BUNDLE_NAME ."
                }
            }
        }

        stage('Deploy to Elastic Beanstalk') {
            steps {
                withCredentials([
                    [$class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'AKIAQKGGW7HMZF3OSE2N', accessKeyVariable: 'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']
                ]) {
                    script {
                        sh "aws s3 cp $SOURCE_BUNDLE_NAME s3://$S3_BUCKET/$SOURCE_BUNDLE_NAME"
                        sh "aws elasticbeanstalk create-application-version --application-name $APPLICATION_NAME --version-label $BUILD_NUMBER --source-bundle S3Bucket=$S3_BUCKET,S3Key=$SOURCE_BUNDLE_NAME"
                        sh "aws elasticbeanstalk update-environment --application-name $APPLICATION_NAME --environment-name $ENVIRONMENT_NAME --version-label $BUILD_NUMBER"
                    }
                }
            }
        }
    }
}
