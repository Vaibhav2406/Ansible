ansible_cmd = ''
pipeline {
    agent any
    
    parameters{
        choice(
        description: 'SelectType'
        name: 'tags'
            choices: ['Pre-deployment','Post-deployment']    
        )
    }
     stages {
        stage('Git Checkout') {
            steps {
              git branch: 'main', url: 'https://github.com/Vaibhav2406/Ansible.git'
            }
           
        }
        stage('Installing tools on slave') {
            steps {
              echo "Selected verification type is: $(params.tags)"
              ansiblePlaybook credentialsId: 'devops', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'Inv', playbook: 'Git.yml'
            }
           
          }
         stage('Service Checking') {
            steps {
              ansiblePlaybook credentialsId: 'devops', disableHostKeyChecking: true , installation: 'Ansible', inventory: 'Inv', playbook: 'ServiceCheck.yml'
            }
           
          }
        
       }
    }
