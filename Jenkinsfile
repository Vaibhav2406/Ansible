pipeline {
    agent any
    parameters {
        choice(
            name: "Verification_Type", choices: ["Pre-verification" , "Post-verification"], description: "Verification")
        choice(
            name: "Nodes", choices: ["xsj1", "xsj2"], description: "target_node")
            
    }

    stages {
        
        stage ('Updating workspace directory') {
            steps {
                dir("~/home/ubuntu/testv/repos/Ansible") {
                    sh "pwd"
                 }
            }
        }
        stage ('Installing Git') {
            when {
                expression { params.Verification_Type == 'Pre-verification' }
            }
            steps {
                ansiblePlaybook credentialsId: 'devops', disableHostKeyChecking: true, installation: 'Ansible', inventory: '../xmpp-xsj-hosts --limit=$Nodes' , playbook: 'Git.yml'
            }
        }
        stage ('Checking Git Version') {
            when {
                expression { params.Verification_Type == 'Post-verification' }
            }
            steps {
                ansiblePlaybook credentialsId: 'devops', disableHostKeyChecking: true, installation: 'Ansible', inventory: '../xmpp-xsj-hosts', playbook: 'ServiceCheck.yml'
            }
        }
    }
}
