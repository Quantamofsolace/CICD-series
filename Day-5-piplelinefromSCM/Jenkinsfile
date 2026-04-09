pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
               git branch: 'main', url: 'https://github.com/CloudTechDevOps/CICD-series.git'
            }
        }
         stage('init') {
            steps {
                dir('Day-5-piplelinefromSCM') {
                  sh  'terraform init'
              
                }
            }
        }
        stage('plan') {
            steps {
               dir('Day-5-piplelinefromSCM') {
                  sh  'terraform plan'
              
                }
            }
        }
        stage('apply') {
            steps {
                dir('Day-5-piplelinefromSCM') {
                  sh  'terraform apply -auto-approve'
              
                }
            }
        }
      
    }
}
