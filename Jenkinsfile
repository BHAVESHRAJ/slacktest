pipeline {
  agent any
  environment{
        BASE_JENKINS_URL = 'http://localhost:8080/'
        BASE_REPO_URL = 'https://github.com/BHAVESHRAJ/slacktest/commit/'
  }

  stages {
    stage('jenkins-start-notification'){
            steps{
                script{

                    if( env.GIT_COMMIT != null ){
                        env.TRUNCATED_GIT_COMMIT = env.GIT_COMMIT.take(10)
                    }else{
                        env.TRUNCATED_GIT_COMMIT = 'not defined'
                    }

                    if( env.GIT_PREVIOUS_SUCCESSFUL_COMMIT != null ){
                        env.TRUNCATED_LAST_SUCCESS_COMMIT = env.GIT_PREVIOUS_SUCCESSFUL_COMMIT.take(10)
                    }else{
                        env.TRUNCATED_LAST_SUCCESS_COMMIT = 'not defined'
                    }
                }

                slackSend (channel: 'pipeline-test', tokenCredentialId: 'slack_id, color: '#1676c9', message: "\n *GD Pipeline Deployment*: \n A deployment started on the *${GIT_LOCAL_BRANCH}* branch  \n\n *Build Number*: \t\t\t\t\t\t *Last Commit*\n ${BUILD_NUMBER}                   \t\t\t\t\t\t <${BASE_REPO_URL}/${GIT_COMMIT}|${TRUNCATED_GIT_COMMIT}> \n *Last Successful Commit* \n <${BASE_REPO_URL}/${GIT_PREVIOUS_SUCCESSFUL_COMMIT}|${TRUNCATED_LAST_SUCCESS_COMMIT}> \n\n To see the status of the deployment please <${BASE_JENKINS_URL}/${GIT_LOCAL_BRANCH}/${BUILD_NUMBER}|*follow this link*> \n ")
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
  }

  post{

        success{
            echo 'The pipeline finish successfully'
            slackSend (color: '#417a2a', message: "\n *GD Pipeline Deployment*: \n The deployment No. *${BUILD_NUMBER}* was successful based on the changes on the *${GIT_LOCAL_BRANCH}* branch \n\n To see the deployment results please <${BASE_JENKINS_URL}/${GIT_LOCAL_BRANCH}/${BUILD_NUMBER}|*follow this link*> \n "), channel: 'pipeline-test', tokenCredentialId: 'slack_id')
        }

        failure{
            echo 'Something went wrong'
            slackSend (color: '#a8120a', message: "\n *GD Pipeline Deployment*: \n The deployment *No.${BUILD_NUMBER}* has errors, please review the *${GIT_LOCAL_BRANCH}* branch \n\n To see the deployment errors please <${BASE_JENKINS_URL}/${GIT_LOCAL_BRANCH}/${BUILD_NUMBER}|*follow this link*> \n "), channel: 'pipeline-test', tokenCredentialId: 'slack_id')
        }
    }    
}
      
    
