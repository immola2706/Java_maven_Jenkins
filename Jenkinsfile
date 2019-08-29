pipeline {
    agent any

    stages {

        stage('SCM Checkout') {
            steps {
                git credentialsId: '2d148d77-32d5-4010-98bb-1b1ff3e6c97d', url: 'https://github.com/immola2706/Java_maven_Jenkins.git'
            }
        }

        stage('Compile Stage') {
            steps {
                withMaven(maven : 'maven_3.6') {
                    sh 'mvn clean compile'
                }
            }
        }


        stage('Test Stage') {
            steps {
                withMaven(maven : 'maven_3.6') {
                    sh 'mvn test'
                }
            }
        }


        stage('Create the Build artifacts Stage (Package)') {
            steps {
                withMaven(maven : 'maven_3.6') {
                    sh 'mvn package'
                }
            }
        }

  /*      stage('Deployment Stage - Tomcat Container') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'cfd6a370-aa88-4ce8-8341-54fe37eab136', path: '', url: 'http://18.218.95.134:9090/')], contextPath: mvn-hello-world, *.war: 'target/*.war'
            }
        }
        
        stage ('Creating AWS S3 Bucket for storing Terraform State') {
            steps {
                sh 'aws s3api create-bucket --bucket bucket-tf-state-49473 --region us-east-2'
                    
                }              
        }
 */

        stage ('Terraform Setup') {
            steps {
                script {
                    def tfHome = tool name: 'Terraform_0.12.6', type: 'org.jenkinsci.plugins.terraform.TerraformInstallation'
                    
                }              
            sh 'terraform --version'                    
                
            }
        }
        stage ('Terraform Init and Plan') {
            steps {
                sh 'terraform init $WORKSPACE'
                sh 'terraform plan'
            }
        }

        stage ('Terraform Apply') {
            steps {
                sh 'terraform apply --auto-approve'               
            }
        }

    }
}
