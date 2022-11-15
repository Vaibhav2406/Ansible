pipeline {
    agent any
    parameters {
        choice(
            choices: ['Pre-verification' , 'Post-verification'],
            description: 'Verification',
            name: 'Verification_Type')
    }

    stages {
        stage ('Installing Git') {
            when {
                expression { params.Verification_Type == 'Pre-verification' }
            }
            steps {
                ansiblePlaybook credentialsId: 'devops', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'Inv', playbook: 'Git.yml' , --limit=xsj2
            }
        }
        stage ('Checking Git Version') {
            when {
                expression { params.Verification_Type == 'Post-verification' }
            }
            steps {
                ansiblePlaybook credentialsId: 'devops', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'Inv', playbook: 'ServiceCheck.yml'
            }
        }
    }
}
