pipeline {
  agent any
  environment{
        BASE_JENKINS_URL = 'http://localhost:8080/'
        BASE_REPO_URL = 'https://github.com/BHAVESHRAJ/test/commit/'
  }

  stages {
    stage ('Start') {
      steps {
        // send build started notifications
        slackSend (color: '#FFFF00', message: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})", channel: 'pipeline-test', tokenCredentialId: 'slack_id')
      }
    }    
    stage("Build") {
      steps {
        echo "building..."
      }
    }
    stage("Test") {
      steps {
        echo "testing..."
      }
    }
    stage("Package") {
      steps {
        echo "packaging..."
      }
    }
    stage("Notification") {
      steps {
        //slackSend channel: '#pipeline', color: '#417a2a', message: 'Pipeline Notification', tokenCredentialId: 'slack_id'
       echo 'The pipeline finish successfully'
        //slackSend (channel: 'pipeline-test', tokenCredentialId: 'slack_id', color: '#417a2a', message: "\n *GDPR Pipeline Deployment*: \n",)
          slackSend(color: '#417a2a', message: "*${currentBuild.currentResult}:* Job `${env.JOB_NAME}` build `${env.BUILD_DISPLAY_NAME}` by <@${env.GIT_AUTHOR}>\n Build commit: ${GIT_COMMIT}\n Last commit message: '${env.GIT_COMMIT_MSG}'\n More info at: ${env.BUILD_URL}\n Time: ${currentBuild.durationString.minus(' and counting')}", channel: 'pipeline-test', tokenCredentialId: 'slack_id')
   // post {
        // Send the build result to slack channel
     //   success {
       //   slackSend (channel: 'pipeline-test', tokenCredentialId: 'slack_id', color:'good', message: "<@$userIds>Successfully deployed")
      //  }
       // failure {
           // slackSend (channel: 'pipeline-test', tokenCredentialId: 'slack_id', color:'danger', message: "<@$userIds>Error in build ${env.JOB_NAME}")
       // }
   // }

     }
    }
  }

  post{

        success{
            echo 'The pipeline finish successfully'
            slackSend (color: '#417a2a', message: "\n *Pipeline Deployment*: \n The deployment No. *${BUILD_NUMBER}* was successful based on the changes on the *${GIT_LOCAL_BRANCH}* branch \n\n To see the deployment results please <${BASE_JENKINS_URL}/${GIT_LOCAL_BRANCH}/${BUILD_NUMBER}|*follow this link*> \n "), channel: 'pipeline-test', tokenCredentialId: 'slack_id')
        }

        failure{
            echo 'Something went wrong'
            slackSend (color: '#a8120a', message: "\n *Pipeline Deployment*: \n The deployment *No.${BUILD_NUMBER}* has errors, please review the *${GIT_LOCAL_BRANCH}* branch \n\n To see the deployment errors please <${BASE_JENKINS_URL}/${GIT_LOCAL_BRANCH}/${BUILD_NUMBER}|*follow this link*> \n "), channel: 'pipeline-test', tokenCredentialId: 'slack_id')
        }
    }    
}
      
    
