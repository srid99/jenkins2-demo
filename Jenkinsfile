node {
    if (env.BRANCH_NAME == 'master') {
        withCredentials([[$class: 'StringBinding', credentialsId: 'master-slack-token', variable: 'SLACK_TOKEN']]) {
            SLACK_CHANNEL = '#build-master'
            SLACK_TEAM_DOMAIN = 'jenkins-testing'
            SLACK_TOKEN = "${SLACK_TOKEN}"
        }
    } else {
        withCredentials([[$class: 'StringBinding', credentialsId: 'develop-slack-token', variable: 'SLACK_TOKEN']]) {
            SLACK_CHANNEL = '#build-develop'
            SLACK_TEAM_DOMAIN = 'jenkins-testing'
            SLACK_TOKEN = "${SLACK_TOKEN}"
        }
    }

    checkout scm

    echo BUILD_APP
    stage 'Build'
    echo 'Build the app'
    
    stage 'Deploy to Test'
    echo 'Deploy the app in Test environment'

    stage 'Test'
    echo 'Test the app'
    notify('Deployed in Test')

    if (env.BRANCH_NAME == 'master') {
	stage 'Release'
	echo 'Release the app'

	stage 'Publish artifact'
	echo 'Publish the released version to a artifact repository'

	stage 'Deploy to Prod'
	echo 'All is well. Let\'s push it to Prod'
        notify('Deployed in Prod')
    }
}

def notify(message) {
    slackSend channel: "${SLACK_CHANNEL}", color: "good", message: "<${env.BUILD_URL}|${env.JOB_NAME} - #${env.BUILD_NUMBER}> - ${message}", teamDomain: "${SLACK_TEAM_DOMAIN}", token: "${SLACK_TOKEN}"
}

