def COLOR_MAP = [
    'SUCCESS': 'good', 
    'FAILURE': 'danger',
    'UNSTABLE': 'danger'
]
pipeline {
    agent any
    stages {
        // Verifying setup
        stage('Confirm Tools Installations') {
            steps {
                sh 'git --version'
                sh 'terraform version'
            }
        }
        // Initialize terraform
        stage('Initialize Terraform Environment') {
            steps {
                sh 'terraform init'
            }
        }
        // Check terraform confugirations syntax
        stage('Validate Terraform Configurations') {
            steps {
                sh 'terraform validate'
            }
        }
        // Generating execution plan
        stage('Generate Terraform Plan') {
            steps {
                sh 'terraform plan'
            }
        }
        // Snyk infrastructure automation test
        stage('SCA') {
            steps {
                snykSecurity(
                  snykInstallation: 'snyk',
                  snykTokenId: 'Snyk-Token-Alert',
                  failOnIssues: false,
                )
            }
        }
        // Checkov infrastructure automation test
        stage('Checkov scan') {
            steps {
                sh 'checkov -d .'
            }
        }
        // Deployment apporval
        stage('Manual Approval') {
            steps {
                input 'Approval Infra Deployment'
            }
        }
        // Deploy terraform infrastructure
        stage('Deploy Infrastructure') {
            steps {
                sh 'terraform apply --auto-approve'
            }
        }
        // // Destroy terraform infrastructure
        // stage('Deploy Infrastructure') {
        //     steps {
        //         sh 'terraform destroy --auto-approve'
        //     }
        // }
    }
    post {
    always {
        echo 'Slack Notifications.'
        slackSend channel: '#terraform-jenkins-cicd-pipeline-project-alerts', //update and provide your channel name
        color: COLOR_MAP[currentBuild.currentResult],
        message: "*${currentBuild.currentResult}:* Job Name '${env.JOB_NAME}' build ${env.BUILD_NUMBER} \n Build Timestamp: ${env.BUILD_TIMESTAMP} \n Project Workspace: ${env.WORKSPACE} \n More info at: ${env.BUILD_URL}"
    }
  }
}