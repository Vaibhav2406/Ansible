pipeline {
    agent any
     stages {
        stage('Git Checkout') {
            steps {
              git branch: 'main', url: 'https://github.com/Vaibhav2406/Ansible.git'
            }
           
        }
        stage('Installing tools on slave') {
            steps {
              ansiblePlaybook credentialsId: 'devops', disableHostKeyChecking: true , --extra-vars '{"tags":"${params.Pre-deployment}"}', installation: 'Ansible', inventory: 'Inv', playbook: 'Git.yml'
            }
           
          }
         stage('Service Checking') {
            steps {
              ansiblePlaybook credentialsId: 'devops', disableHostKeyChecking: true , installation: 'Ansible', inventory: 'Inv', playbook: 'ServiceCheck.yml'
            }
           
          }
        
       }
    }
