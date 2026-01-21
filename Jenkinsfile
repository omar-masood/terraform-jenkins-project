pipeline {
    agent any

    // Pass AWS credentials to Terraform
    environment {
        AWS_ACCESS_KEY_ID     = credentials('aws-access-key')      // Jenkins global credential ID
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-key')     // Jenkins global credential ID
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/omar-masood/terraform-jenkins-project.git'
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Terraform Validate') {
            steps {
                sh 'terraform validate'
            }
        }

        stage('Terraform Plan') {
            steps {
                sh 'terraform plan'
            }
        }

        stage('Approval') {
            steps {
                input message: 'Do you want to apply this Terraform plan?',
                      ok: 'Approve & Apply'
            }
        }

        stage('Terraform Apply') {
            steps {
                sh 'terraform apply'
            }
        }
    }
}
