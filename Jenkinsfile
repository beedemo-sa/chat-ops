pipeline {
    agent none
    stages {
        stage ('Notify') {
            steps {
                echo "Prompting for approval"
            }
            post {
                success {
                    slackSend color: 'green', message: "${JOB_NAME} pipeline job is awaiting approval at: ${RUN_DISPLAY_URL}"
                }
            }
        }
        stage('Deploy') {
          options {
            timeout(time: 300, unit: 'SECONDS') 
          }
          input {
            message "Should we deploy?"
            submitterParameter "APPROVER"
          }
          steps {
            echo "Continuing with deployment - approved by ${APPROVER}"
          }
          post {
            success {
                slackSend color: 'green', message: "${JOB_NAME} has completed deployment. View here: ${RUN_DISPLAY_URL}, approved by ${APPROVER}"
            }
          }
        }
    }
}
