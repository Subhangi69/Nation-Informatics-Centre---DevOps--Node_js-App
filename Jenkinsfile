pipeline {
    agent any

    environment {
        AWS_REGION = 'ap-southeast-2'
        APPLICATION_NAME = 'nodejg'
        ENVIRONMENT_NAME = 'Nodejg-env'
        S3_BUCKET = 'elasticbeanstalk-ap-southeast-2-021891578329'
        SOURCE_BUNDLE_NAME = 'nodejs-app.zip'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/Subhangi69/National-Informatics-Centre---DevOps'
            }
        }

        stage('Install Dependencies & Test') {
            steps {
                sh 'npm install'
                sh 'chmod +x ./node_modules/.bin/mocha' // fix mocha permission
                sh 'npm test' // OR use: sh './node_modules/.bin/mocha'
            }
        }

        stage('Package App') {
            steps {
                sh "zip -r $SOURCE_BUNDLE_NAME ."
            }
        }

        stage('Deploy to AWS Elastic Beanstalk') {
            steps {
                withCredentials([
                    [$class: 'AmazonWebServicesCredentialsBinding',
                     credentialsId: 'subhangi-aws-creds',
                     accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                     secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']
                ]) {
                    sh "aws s3 cp $SOURCE_BUNDLE_NAME s3://$S3_BUCKET/$SOURCE_BUNDLE_NAME"
                    sh "aws elasticbeanstalk create-application-version --application-name $APPLICATION_NAME --version-label $BUILD_NUMBER --source-bundle S3Bucket=$S3_BUCKET,S3Key=$SOURCE_BUNDLE_NAME"
                    sh "aws elasticbeanstalk update-environment --application-name $APPLICATION_NAME --environment-name $ENVIRONMENT_NAME --version-label $BUILD_NUMBER"
                }
            }
        }
    }
}
